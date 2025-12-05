# 75. Sort Colors

- 배열의 원소는 0, 1, 2 라는 값만 가짐
- 퀵소트로 한 번만 배열을 훑고 지나가면 정렬 완성 (pivot=1)
- 신경써야 할 점: pivot이 여러 개 나올 수 있음


## 풀이

- small: pivot과 같은 값 영역 중에서 제일 작은 인덱스. 이 앞은 pivot보다 작은 영역이므로, pivot보다 작은 값이 나오면 이 값과 위치를 바꿔준다.
- equal: pivot과 같은 값 영역 중에서 제일 큰 인덱스. 
- large: pivot보다 큰 값 영역. 배열의 마지막 인덱스부터 시작하는 위치로, pivot보다 큰 값이 나오면 이곳으로 보낸다. 

``` java

  public void sortColors(int[] nums) {
        int pivot=1;
        int small=0;
        int equal=0;
        int large=nums.length-1;

        while(equal<=large){
            if(nums[equal]<pivot){
                swap(nums, small, equal);
                small++;
                equal++;
            }
            else if(nums[equal]==pivot){
                equal++;
            }
            else {
                swap(nums, equal, large);
                large--;
            }
        }
  }
```

