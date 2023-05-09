### 이분탐색

		while (left <= right) {
			mid = (left + right) / 2;

			if (num[mid] == select) {
				System.out.println(1);
				check = true;
				break;
			}
			if (select < num[mid]) {
				right = mid - 1;
			} else if (select >= num[mid]) {
				left = mid + 1;
			}

		}

### PriorityQueue
	PriorityQueue<Time> q = new PriorityQueue();

	static class Time implements Comparable<Time> {
        int start;
        int end;

        public Time(int start, int end) {
            this.start = start;
            this.end = end;
        }

        @Override
        public int compareTo(Time o) {
            return this.start - o.start;
        }
    }

### 정렬
	  // List
        Collections.sort(bookList,(o1,o2)->{
            if(o1.start_time==o2.start_time) return o1.end_time-o2.end_time;
            else return o1.start_time-o2.start_time;
        });
	
	// 배열
	Arrays.sort(bookList,(o1,o2)->{
            if(o1.start_time==o2.start_time) return o1.end_time-o2.end_time;
            else return o1.start_time-o2.start_time;
        });
	
	
### dfs 


### 조합 n개중 r개 뽑기
 // n = 29 r = 13
    static public double comb(double n, double r ){
        double a = 1;
        double b = 1;

        for (double i = n; i > n - r; i--) {
            a = a * i;
        }

        for (double i = r; i > 0; i--) {
            b = b * i;
        }
        
        return a/b;
    }
