# Meeting Rooms

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
	
     public static class IntervalComparator implements Comparator<Interval>{
	  public int compare(Interval a, Interval b){
	      Integer ai = new Integer(a.start);
	      Integer bi = new Integer(b.start);
	      return ai.compareTo(bi);
	  }
     }
	
     public static boolean canAttendMeetings(List<Interval> intervals) {
        if(intervals == null){
            return false;
        }
        if(intervals.size() <= 1){
            return true;
        }
        
        intervals.sort(new IntervalComparator());
        int lastMeetingEnd = intervals.get(0).end;
        
        for(int i = 1; i < intervals.size(); i++){
            Interval interval = intervals.get(i);
            if(lastMeetingEnd > interval.start){
                return false;
            }
            lastMeetingEnd = interval.end;
        }
     
        return true;
      }

}

```
