---
title:  simple BFS via golang
layout: single
author_profile: true
comments: true
share: true
related: false
date: '2018-10-18'
tags:
    - golang
    - algorithm
    - python
    - quicksort
category: algorithm
---

## simple BFS via golang 

### Why write this
* 최근 틈틈이 알고리즘 책을 읽고 있습니다. 
* 여러가지 알고리즘을 읽고 있지만 본의 아니게 파이썬으로 설명하는 책을 많이 읽게 되었습니다. 
* 파이썬으로는 너무나도 간단하게 구현 되는 경우가 많습니다. 
* 그러다 보니 이거 golang 으로 작성하면 어떻게 되지? 라는 의문을 가지게 됩니다. 


### 들어가기 전에 
- BFS를 python으로 이해하고 나니 golang 에서는 어떻게 구현이 될지 궁금 합니다. 
    - python 코드는 3.x에서 동작 합니다. 
    - 해당 알고리즘책은 아래와 같습니다. 
    - BFS => Breadth-first search
### Reference
* [Hello Coding 그림으로 개념을 이해하는 알고리즘](https://book.naver.com/bookdb/book_detail.nhn?bid=11823284) - 한빛 미디어

### 우선 기존의 python 코드를 보겠습니다. 
<pre>
<code>
from collections import deque



def search(name):
    search_queue=deque()
    search_queue+=graph[name]
    searched=[]
    while search_queue:
        person= search_queue.popleft()
        print(person+" pop name")
        if not person in searched:
            if person_is_seller(person):
                print(person+" is a mango seller!")
                return True
            else:
                search_queue+=graph[person]
                searched.append(person)
    return False

def person_is_seller(name):
    return name[-1]=='m'

graph={}
graph["you"]=["alice","bob","claire"]
graph["bob"]=["anuj","peggy"]
graph["alice"]=["peggy"]
graph["claire"]=["thom","jonny"]
graph["anuj"]=["slime"]
graph["peggy"]=[]
graph["thom"]=[]
graph["johny"]=[]


search("you")
</code>
</pre>
### 코드는 you 라는 시작점부터 시작합니다. 
- 목표는 m 으로 끝나는 사람을 찾는 겁니다. 
    - 해당 조건은 취향에 맞춰서 바꿀수 있습니다. 
- 책에서는 그림으로 보여 주었지만 방향성이 따로 없다는 것 으로 생각 했을때 tree 형태로 보여줘도 문제 없다고 판단되어서 아래와 같이 그림으로 대체 합니다. 
* * *
|![treeForBFS](/assets/images/static/2018-10-18/bfsTreeArchi.png){: width="50%" height="50%"}|
- python 에서는 간단하게 hash table (map)을 만듭니다.

### 설명 전에 
- 코드를 만드는 중에 2가지 정도의 딜레이 사항이 있었는데요 
    1. 하나는 golang 에서는 기본적으로 queue 라는 구조가 없더군요. (왜지?)
        - 아래와 같이 [golang.org doc](https://golang.org/pkg/container/) 에는 queue 를 제외하고 있네요. 
            - heap	Package heap provides heap operations for any type that implements heap.Interface.
            - list	Package list implements a doubly linked list.
            - ring	Package ring implements operations on circular lists.
    2. 두번째는 hash table 형태를 만드는 거였습니다. 
        - key, value 형태에서의 array 느낌이 조금 달라서.. 
### golang 으로 만들어 봅시다
- 우선은 python 에서의 graph 를 만들어 봐야 겠군요.
    - golang 에서는 map 이라는 자로구조 가 있으니까 이걸 활용 해 봅니다.
    - key 와 value 가 모두 string 의 형태 이고 value 에 대해서는 key 에 대해서는 배열로 값을 가지고 있습니다. 
        - 사실 이 부분에서 조금 시간이 지체되었습니다. 
        - 아루래도 다른 언어로 변환 하다 보니 그대로 가져 갈수 없는 부분들이 있어서..
        - stacoverflow 에 비슷한 고민을 한 글이 있어서 참고 했습니다. 
            - https://stackoverflow.com/questions/4286615/how-do-i-create-a-map16bytestring-in-go
            - 해당 글은 정확히는 중간에 []가 uri 를 만드는 과정에서 없어져서 구글 검색이 안되거나 주소로 해당 페이지를 찾을수 없을수 있습니다. 
            - 위의 글을 검색하고 싶다면 다음의 문장을 google 에서 검색하에요.
            - How do I create a map[[16]byte][]string in Go 

<pre><code>
	graph := make(map[string][]string)
	graph["you"] = []string{"alice", "bob", "claire"}
	// https: //stackoverflow.com/questions/4286615/how-do-i-create-a-map16bytestring-in-go
	graph["bob"] = []string{"anju", "peggy"}
	graph["alice"] = []string{"peggy"}
	graph["claire"] = []string{"thom", "jonny"}
	graph["anju"] = []string{}
	graph["peggy"] = []string{}
	graph["thom"] = []string{}
	graph["johny"] = []string{}
</code></pre>

- 그 다음은 search func 를 만들어 보겠습니다. 
    - queue 는 결국 어디서 꺼내느냐의 차이 이기 때문에 append 와 slice 로 대체 했습니다. 
    - contains golang.org 를 찾아 봤지만 찾지 못했기 때문에 간단하게 만들었습니다. 
<pre><code>
func search(name string, graph map[string][]string) bool {

	var search_queue = []string{}

	search_queue = append(search_queue, graph[name]...)
	var serarched = []string{}

	for len(search_queue) > 0 {
		person := search_queue[len(search_queue)-1 : len(search_queue)]
		search_queue = search_queue[:len(search_queue)-1]
		//pop
		fmt.Println(person[0] + " is a pop")
		if !Contains(serarched, person[0]) { // Contains() 를 만들었다.
			fmt.Println("inner contains")
			if person_is_sellor(person[0]) {
				fmt.Println(person[0] + " is a mango seller!")
				return true
			} else {
				search_queue = append(search_queue, graph[person[0]]...)
				serarched = append(serarched, person[0])
			}
		}

	}
	return false
}

</code></pre>
* 전체 코드를 첨부 합니다. 
    - 웹에서는 
    - https://go-tour-kr.appspot.com/#1 
    - 주소에서도 테스트 가능 합니다.  
<pre><code>
package main

import (
	"fmt"
	"strings"
)

func Contains(a []string, x string) bool {
	for _, n := range a {
		if x == n {
			return true
		}
	}
	return false
}

func search(name string, graph map[string][]string) bool {

	var search_queue = []string{}

	search_queue = append(search_queue, graph[name]...)
	var serarched = []string{}

	for len(search_queue) > 0 {
		person := search_queue[len(search_queue)-1 : len(search_queue)]
		search_queue = search_queue[:len(search_queue)-1]
		//pop
		fmt.Println(person[0] + " is a pop")
		if !Contains(serarched, person[0]) {
			fmt.Println("inner contains")
			if person_is_sellor(person[0]) {
				fmt.Println(person[0] + " is a mango seller!")
				return true
			} else {
				search_queue = append(search_queue, graph[person[0]]...)
				serarched = append(serarched, person[0])
			}
		}

	}
	return false
}
func person_is_sellor(name string) bool {

	return strings.EqualFold(name[len(name)-1:len(name)], "m")

}
func main() {

	graph := make(map[string][]string)
	graph["you"] = []string{"alice", "bob", "claire"}
	// https: //stackoverflow.com/questions/4286615/how-do-i-create-a-map16bytestring-in-go
	graph["bob"] = []string{"anju", "peggy"}
	graph["alice"] = []string{"peggy"}
	graph["claire"] = []string{"thom", "jonny"}
	graph["anju"] = []string{}
	graph["peggy"] = []string{}
	graph["thom"] = []string{}
	graph["johny"] = []string{}

	fmt.Println(search("you", graph))
}


</code></pre>

## 마치며 
* golang 의 좋은 점을 알리고 싶어서 쓰고 있는 글인데 왠지 python 의 더 간단한 점을 보여주고 있는거 같네요.
* 그래도 golang 의 static 함은 좋은 거 같습니다. 오류나 애매한 부분을 거의 대부분 제거해 버리는 부분 같은거 


