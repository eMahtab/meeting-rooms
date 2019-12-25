# Meeting Rooms

Given an array of meeting time intervals consisting of start and end times [[s1,e1],[s2,e2],...] (si < ei), determine if a person could attend all meetings.

```
Example 1

Input: intervals = [(0,30),(5,10),(15,20)]
Output: false
Explanation: 
(0,30), (5,10) and (0,30),(15,20) will conflict

Example 2

Input: intervals = [(5,8),(9,15)]
Output: true
Explanation: 
Two times will not conflict 

Notice : (0,8),(8,10) is not conflict at 8
```
### Implementation


```java
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;

class Interval {
	int start, end;

	Interval(int start, int end) {
		this.start = start;
		this.end = end;
	}
}

public class App {
	public static void main(String[] args) {
		List<Interval> meetings = new ArrayList<Interval>();
		meetings.add(new Interval(0, 30));
		meetings.add(new Interval(5, 10));
		meetings.add(new Interval(15, 20));
		System.out.println(canAttendMeetings(meetings));
	}

	public static class IntervalComparator implements Comparator<Interval> {
		public int compare(Interval a, Interval b) {
			return a.start - b.start;
		}
	}

	public static boolean canAttendMeetings(List<Interval> intervals) {
		if (intervals == null) {
			return false;
		}
		if (intervals.size() <= 1) {
			return true;
		}

		intervals.sort(new IntervalComparator());
		for (int i = 0; i < intervals.size() - 1; i++) {
			if (intervals.get(i).end > intervals.get(i + 1).start) {
				return false;
			}
		}

		return true;
	}

}

```
