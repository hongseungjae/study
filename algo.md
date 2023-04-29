** 이분탐색

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
