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
