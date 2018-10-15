---
title: golang 으로 만들어 보는 지뢰찾기 게임 
layout: single
author_profile: true
comments: true
share: true
related: false
date: '2018-10-10'
tags:
    - golang
    - mine_game
    - algorithm
category: golang
---

## golang 으로 만들어 보는 지뢰찾기 게임 알고리즘(mine_game algorithm)

취업 활동 중에 지뢰찾기 과제를 받게 되어서 관련한 글을 올려 봅니다. 
관련해서 찾아 보니까 JAVA 로는 비슷한 글들이 많던데요. 전 최근에 golang 을 많이 쓰고 있으니까 golang 으로 만들어 봤습니다. 

### 최종 목표는 
1. 10 * 10 크기의 지뢰판 
2. 10개의 지뢰가 랜덤하게 배치 
3. 해당 지뢰를 기준으로 100개의 모든 상자에 숫자를 기록하기 

우선 3 * 3 부터 시작을 합니다. 대략적인 그림을 그리기 위해서 임의로 지뢰를 배치하고 어떻게 숫자를 넣어야 할지 확인 했습니다. 

<pre>
    _ 는 지뢰가 없는 부분 * 는 지뢰가 있는 부분 입니다. 
    그렇다면 

    _ _ *
    _ _ * 
    * _ _ 
    
    위와 같은 3 * 3 의 지뢰판이 있다면 
    
    숫자로 나타내면 

    0 2 1 
    1 3 1
    0 2 1 

    이와 같은 형태가 됩니다. 

    지뢰가 있는 부분도 주위의 지뢰의 갯수를 세서 나타 냈습니다. 
    위의 경우는 2차원의 배열로 나타내면 

    (0,0) (0,1) (0,2)
    (1,0) (1,1) (1,2)
    (2,0) (2,1) (2,2)

    위와 같은 형태가 됩니다. 

    뭔가 규칙이 보이시나요? 

    (1,1) 을 기준으로 총 8개의 경우가 있고 (1,1) 을 기준으로 -1, 0, 1 을 row, col 에 대해서 가감을 통한 것들이 좌표 입니다. 
    ( 2개의 자리에 대해서 각각 3가지의 경우의 수 2^3 => 8 이니까 )
    물론 (0,0) 이나 (2,2) 같은 모서리나 끝부분에 있는 부분은 예외 입니다. 

    지뢰판은 0~ 지뢰판의 크기-1  / 여기서는 0~2 가 되겠군요. 
    해당 하는 부분을 예외 처리 하도록 합니다. 프로그램은 예외처리가 제일 중요하다고 생각합니다. 

    그러니까 간단하게 생각하면 for 문을 여러번 돌려서 매 좌표 마다 주위의 지뢰 갯수를 세서 해당 좌표에 넣어 주면 완성 입니다. 

    일단 대략적인 flow는 생각 해 봤으니까 하나씩 구현해 볼까요 
</pre>
[1] 우선 최초에 지뢰찾기 필드의 크기가 정해지면 해당 부분을 초기화 해야 겠죠
<pre>
<code>
func initMindField() {
	for i := 0; i < len(mineCountInfo); i++ {
		for j := 0; j < len(mineCountInfo[i]); j++ {
			mineInfo[i][j] = "_"
		}

	}
}
</code>
</pre>
[2] 그리고 나면 랜덤하게 지뢰찾기 필드에 지뢰를 깔아 봅시다
<pre>
<code>
func mineDeploy() {
	tempmineCnt := mineCount
	s3 := rand.NewSource(time.Now().UnixNano()) // seed 값을 유닉스 타임스탬프로 설정 함으로서 매 시간마다 다른 값이 나오게 설정
	r3 := rand.New(s3)
	for tempmineCnt > 0 {
		tempmineCnt--
		row := r3.Intn(MineMapsize)
		col := r3.Intn(MineMapsize)
		if strings.EqualFold(mineInfo[row][col], "*") {
			tempmineCnt++
		}
		if strings.EqualFold(mineInfo[row][col], "_") {
			mineInfo[row][col] = "*"
		}
	}

}
</code>
</pre>
[3] 지뢰가 모두 깔리고 나면 이제부터 전체적인 지뢰찾기 필드에 숫자를 채워 봅시다.
<pre>
<code>
func processSetNumber() {
	for i := 0; i < len(mineInfo); i++ {
		for j := 0; j < len(mineInfo[i]); j++ {

			mineCountInfo[i][j] = getMineNumber(i, j)

		}

	}
}
func getMineNumber(row int, col int) int {
	tempmineCnt := 0
	// 2^3 8 가지 경우의 수

	for i := -1; i < 2; i++ {
		for j := -1; j < 2; j++ {
			if !(i == 0 && j == 0) { // 본인의 좌표는 제외
				if isMineExist(row+i, col+j) {
					tempmineCnt++
				}
			}

		}
	}

	// 좌표를 주고 그 좌표의 8방향에 대해서의 지뢰 갯수를 세고 해당 지뢰 갯수를 리턴
	return tempmineCnt
}
func isMineExist(row int, col int) bool {

	if row < 0 || row >= MineMapsize || col < 0 || col >= MineMapsize {
		// 지점에서 8 방향 중에 좌표를 벗어나면 false 처리 한다.
		return false
	}

	return strings.EqualFold(mineInfo[row][col], "*")
}
</code>
</pre>

[4] 이것을 전체 소스로 보면 아래와 같습니다. / golang 은 시스템 패키지 같은 경우는 자동으로 import 됩니다. 


<pre>
<code>
package main

import (
	"fmt"
	"math/rand"
	"strconv"
	"strings"
	"time"
)

// 지뢰판 크기 정하기
const MineMapsize = 10

// 좌표 별 주위의 mine  갯수를 담을 배열
var mineCountInfo [MineMapsize][MineMapsize]int

// mine 위치 정보 담을 배열
var mineInfo [MineMapsize][MineMapsize]string

const mineCount = 10 // 지뢰 갯수

func getMineNumber(row int, col int) int {
	tempmineCnt := 0
	// 2^3 8 가지 경우의 수

	for i := -1; i < 2; i++ {
		for j := -1; j < 2; j++ {
			if !(i == 0 && j == 0) { // 본인의 좌표는 제외
				if isMineExist(row+i, col+j) {
					tempmineCnt++
				}
			}

		}
	}

	// 좌표를 주고 그 좌표의 8방향에 대해서의 지뢰 갯수를 세고 해당 지뢰 갯수를 리턴
	return tempmineCnt
}
func isMineExist(row int, col int) bool {

	if row < 0 || row >= MineMapsize || col < 0 || col >= MineMapsize {
		// 지점에서 8 방향 중에 좌표를 벗어나면 false 처리 한다.
		return false
	}

	return strings.EqualFold(mineInfo[row][col], "*")
}

func mineDeploy() {
	tempmineCnt := mineCount
	s3 := rand.NewSource(time.Now().UnixNano()) // seed 값을 유닉스 타임스탬프로 설정 함으로서 매 시간마다 다른 값이 나오게 설정
	r3 := rand.New(s3)
	for tempmineCnt > 0 {
		tempmineCnt--
		row := r3.Intn(MineMapsize)
		col := r3.Intn(MineMapsize)
		if strings.EqualFold(mineInfo[row][col], "*") {
			tempmineCnt++
		}
		if strings.EqualFold(mineInfo[row][col], "_") {
			mineInfo[row][col] = "*"
		}
	}

}

func initMindField() {
	for i := 0; i < len(mineCountInfo); i++ {
		for j := 0; j < len(mineCountInfo[i]); j++ {
			mineInfo[i][j] = "_"
		}

	}
}
func processSetNumber() {
	for i := 0; i < len(mineInfo); i++ {
		for j := 0; j < len(mineInfo[i]); j++ {

			mineCountInfo[i][j] = getMineNumber(i, j)

		}

	}
}

func main() {

	// 지뢰 찾기 실행 전 지뢰 판 초기화
	initMindField()

	// 지뢰 찾기 시에 임의의 위치에 지뢰 위치 설정
	mineDeploy()

	// mine 위치 최초에 보여주기
	fmt.Println("mine 위치")
	for i := 0; i < len(mineInfo); i++ {
		for j := 0; j < len(mineInfo[i]); j++ {
			fmt.Print(mineInfo[i][j] + " ")
		}
		fmt.Println()

	}

	// mine 위치 를 기준으로 모든 필드에 숫자 값 채우기
	processSetNumber()

	fmt.Println("mine 에 따른 숫자")
	for i := 0; i < len(mineCountInfo); i++ {
		for j := 0; j < len(mineCountInfo[i]); j++ {

			fmt.Print(strconv.Itoa(mineCountInfo[i][j]) + " ")

		}
		fmt.Println()

	}

}
</code>
</pre>

[5] 아래는 해당 파일을 실행 한 스크린 샷 입니다. 
* * *
|![MineGameScreenShot](/assets/images/static/2018-10-10/MineGame_ScreenShot.png){: width="50%" height="50%"}|

<pre>
# 사실 이 부분은 대부분 비슷한 방법으로 해결이 되기 때문에 다른 방법을 좀 더 생각해 보려고도 하고 
  뭔가 golang 의 특징을 좀 더 쓸수 있는 것이 있을까 하고 고민하고 만들 었는데요. 
  아직은 발견하지 못한거 같아요. 
  좀 더 좋은 코드나 golang 의 특징이 반영된 알고리즘을 알고 계시면 공유 해주시면 감사하겠습니다!
</pre>


