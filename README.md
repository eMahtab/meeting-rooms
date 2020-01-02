# Meeting Rooms
## https://www.lintcode.com/problem/meeting-rooms
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
## Approach :
Suppose you have lot of meetings, for example lets say 10 meetings on a particular day. Now you want to make sure, no two meetings overlap, overlap means a second meeting starts while a previous meeting is still going on. If this happens, it means the person can not attend both the mettings. So to solve this problem, we just have to find if there is an overlap between any of the given meetings. If we find an overlap we will retutn false. If there is no overlap between any of the meetings time, it means the person can attend all the meetings, so we will return true for this case.

**Note : We are given that start time of a meeting will always be less than the end time of the meeting. And also if a meeting ends at,  say 2, the person can attend a next meeting that start from 2, it is not considered as an overlap.** 

We can solve this problem, by first sorting all the meetings according to their start times.
After sorting just iterate over all the meetings, and check if the next meeting's start time is less than previous meeting's end time. If thats the case, it means there is an overlap between meetings time, so we return false, but if we don't find an overlap we return true, which means there is no overlap and the person can attend all the meetings.

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
Above implementation have runtime complexity of O(nlogn) and space complexity of O(1)

```
Runtime Complexity = O(nlogn)
Space Complexity   = O(1)
```

