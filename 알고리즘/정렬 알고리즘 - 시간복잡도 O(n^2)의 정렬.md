# sort 알고리즘 - 시간복잡도 O(n^2) 알고리즘

정렬 알고리즘에 대해서 정리하고자 한다.

여기서는 시간복잡도가 O(n^2)인 정렬 알고리즘인 bubble sort, insertion sort, selection sort에 대해 다루고자 한다.

모든 예제는 python3 버전을 기준으로 한다.

## bubble sort

bubble sort 는 다음의 순서대로 동작하는 알고리즘이다.

1. 정렬되지 않은 list를 입력받는다.
2. 앞에서부터 차례대로 2개씩 비교하여 작은(큰)수를 뒤로 보낸다. (2번째 3번째 -> 3번째 4번째 -> 4번째 5번째의 방식 )
3. 한번 끝가지 간다면, 가장 작은(큰)수가 제일 뒤로 갈 것이다.
4. 뒤로 뺀 값을 제외한 list에서 이를 반복한다.

정렬 방식 사진 추가 필요.

bubble sort 만의 장점이라고 한다면, 구현하는 코드가 매우 단순하다는 것이다.

~~~python
input_array = input().split()

array_count = len(input_array)

for i in range(array_count):
	for j in range(1, array_count-i):
		if int(input_array[j-1]) < int(input_array[j]):
			temp = input_array[j-1]
			input_array[j-1] = input_array[j]
			input_array[j] = temp

print(input_array)
~~~



## insertion sort

insertion sort 는 다음의 순서대로 동작하는 알고리즘이다.

1. 정렬된 list를 가진다(정렬되지 않은 상태라면 이 list는 비어있는 상태일 것이다)
2. 정렬 해야하는 목록이나 실시간으로 들어오는 값을 보고, 정렬된 list와 비교해 맞는 장소에 넣는다.
3. 이 과정을 반복한다.

아래 코드는 정렬된 결과인 output을 insertion sort 알고리즘을 이용해 채워나가는 코드이다.

~~~python
input_array = input().split()

array_count = len(input_array)

output = []

output.insert(0, input_array[0])

for i in range(1, array_count):
	for j in range(len(output)):
		if int(output[len(output)-1]) > int(input_array[i]):
			output.insert(len(output), input_array[i])
			break
		if int(output[j]) < int(input_array[i]):
			output.insert(j, input_array[i])
			break

print(output)
~~~



## selection sort

selection sort 는 다음의 순서대로 동작하는 알고리즘이다.

1. list에서 가장 작은(큰) 수를 찾는다.
2. 그렇게 찾은 값을 list의 앞(뒷)부분과 교체한다.
3. 교체한 부분을 뺀 나머지 list에 대해 반복한다.

아래의 코드는 찾은 값을 list의 뒤로 보내면서 정렬을 완료하는 selection sort 코드이다.

~~~python
input_array = input().split()

array_count = len(input_array)

for i in range(array_count):
	max = 0
	for j in range(1, array_count - i):
		if int(input_array[max]) < int(input_array[j]):
			max = j
	
	temp = input_array[max]
	input_array[max] = input_array[array_count - 1 - i]
	input_array[array_count - 1 - i] = temp

print(input_array)
~~~

