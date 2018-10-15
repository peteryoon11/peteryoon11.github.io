---
title:  simple Quicksort via golang
layout: single
author_profile: true
comments: true
share: true
related: false
date: '2018-10-12'
tags:
    - golang
    - algorithm
    - python
    - quicksort
category: algorithm
---

## simple Quicksort via golang

### Why write this
* 최근 틈틈이 알고리즘 책을 읽고 있습니다. 
* 여러가지 알고리즘을 읽고 있지만 본의 아니게 파이썬으로 설명하는 책을 많이 읽게 되었습니다. 
* 파이썬으로는 너무나도 간단하게 구현 되는 경우가 많습니다. 
* 그러다 보니 이거 golang 으로 작성하면 어떻게 되지? 라는 의문을 가지게 됩니다. 

### 그래서 만들어 봤습니다. 

- 가장 많이 쓰이는 quick sort 를 python으로 만든 부분을 보면 참 간단하게 보인다 라는 생각이 듭니다.  
    - 여기서는 pivot 선정 부분에 대해서는 다루지 않습니다. 
    - python 코드는 3.x에서 동작 합니다. 
    - 해당 알고리즘책은 아래와 같습니다. 

### Reference
* [Hello Coding 그림으로 개념을 이해하는 알고리즘](https://book.naver.com/bookdb/book_detail.nhn?bid=11823284) - 한빛 미디어

<pre>
<code>
def quicksort(array):
    if len(array) < 2 :
        return array
    else:
        pivot=array[0]
        less=[i for i in array[1:] if i <pivot]
        greater = [i for i in array[1:] if i> pivot]
        return quicksort(less)+[pivot]+quicksort(greater)


print(quicksort([10,5,2,3]))

</code>
</pre>

- 우리는 golang 으로 구성해 보겠습니다. 
<pre>
<code>
package main

import (
	"fmt"
)

func quicksort(array []int) []int {
	if len(array) < 2 {
		return array
	} else {
		pivot := array[0]
		var less []int
		var greater []int
		for _, i := range array[1:] {
			if i <= pivot {
				less = append(less, i)
			}
		}
		for _, i := range array[1:] {
			if i > pivot {
				greater = append(greater, i)
			}
		}
        // 이 부분이 문제 입니다. 
        // python 에서는 아래와 같이 간단하게 끝나는 부분이 golang 에서는 그렇지 않게 됩니다. 
        // return quicksort(less)+[pivot]+quicksort(greater) 

    }
}
func main() {
	temp := []int{2, 5, 1, 10, 12, 9, 3}
	fmt.Println(quicksort(temp))

}
</code>
</pre>
* 자 그러면 우리는 위의 문제를 어떻게 풀어야 할까요? 파이썬은 느슨한 편이기 때문에(?) 타입에 대한 스트레스를 적게 받는 편이지만 
우리가 쓰려고 하는 golang 은 엄격한 편이지요..
그래서 이런 방법을 써 보았습니다. 
<pre>
<code>
        var temp []int
        return append(temp, quicksort(less),[pivot],quicksort[greater])
</code>
</pre>
* 그렇지만 이렇게 코드를 작성하면 golang 에서는 친절하게 에러라고 알려줍니다... 
    - syntax error: unexpected comma, expecting type <=  이런 에러를 noti 해주십니다...
    - 그렇다면 무엇이 문제 일까? 
    - golang 의 문서를 보았습니다. 
    - https://tour.golang.org/moretypes/15
    - append 하려는 대상이 배열이라 안되는거 같네요.
    - 그럼 여기서 어떻게 해야 하지... 
    - google 에 how to append array to array in golang 라고 검색해 봤습니다. 
    - 역시... 첫번째로 stackvoverflow 의 글이 반겨 줍니다. (저만 이런 의문을 가진게 아니라 다행이네요.)
    - stackvoverflow 에서 vote 를 가장 많이 받은 글을 보니 이해가 됩니다. 
    - https://stackoverflow.com/a/16248257 
    - ecmascript 6 에서도 비슷한 문법을 사용 했던거 같은데요. 
    - vote 를 가장 많이 받은 답변으로 수정해 보았습니다. 
<pre>
<code>
        var temp []int
        
		temp = append(temp, quicksort(less)...)
		temp = append(temp, pivot)
		temp = append(temp, quicksort(greater)...)
        return temp
</code>
</pre>
* 뭔가... 줄이 길어 졌습니다.. golang을 썼는데 python 보다 줄이 길어 졌네요.. 
    - 다른 답변들을 봤습니다. 조금 더 효율적인 방법이 없을까 하고.. 
    - https://stackoverflow.com/a/52642630 
    - 이런 답변이 있네요 이 부분을 응용해 보겠습니다. 
    - 1 줄로 변했습니다! 조금 복잡해 진건.. 기분 탓... 
    - 어느 부분이 좀 더 효울적인지는 다른 포스트에서 확인을 해보도록 하겠습니다. 
<pre>
<code>
    return append([]int{}, append(append(less, pivot), quicksort(greater)...)...)
</code>
</pre>

* 전체 코드를 첨부 합니다. 
    - 웹에서는 
    - https://go-tour-kr.appspot.com/#1 
    - 주소에서도 테스트 가능 합니다. 

<pre>
<code>
    package main

import (
	"fmt"
)

func quicksort(array []int) []int {
	if len(array) < 2 {
		return array
	} else {
		pivot := array[0]
		var less []int
		var greater []int
		for _, i := range array[1:] {

			
			if i <= pivot {
				less = append(less, i)
			}
		}
		for _, i := range array[1:] {
			if i > pivot {
				greater = append(greater, i)
			}
		}
		/* var temp []int

		temp = append(temp, quicksort(less)...)
		temp = append(temp, pivot)
		temp = append(temp, quicksort(greater)...)
		*/
		//return append(quicksort(less),[pivot] , quicksort(greater)...)
		return append([]int{}, append(append(less, pivot), quicksort(greater)...)...)
		//https://stackoverflow.com/questions/16248241/concatenate-two-slices-in-go
	}
}
func main() {
	temp := []int{2, 5, 1, 10, 12, 9, 3}
	fmt.Println(quicksort(temp))

}

</code>
</pre>