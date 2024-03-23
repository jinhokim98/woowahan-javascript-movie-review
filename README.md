# 기능 구현 요구사항

## 영화 목록 조회

- 영화 목록의 1페이지를 불러온다.
  - 한 페이지는 20개씩 영화 목록을 보여준다. (4 x 5)
  - 더보기를 누른 경우, 이후의 영화 목록을 불러온다.
    - _20개를 더 불러오는 동안, Skeleton UI로 보여준다._
    - _로딩 중인 경우, 더보기 버튼은 비활성화 된다._
  - (_불러올 영화가 더 없는 경우_) 경우에는 더보기 버튼을 화면에 출력하지 않는다.
    - _버튼을 변경하여 목록의 끝을 보여주는 ux writing을 출력한다._
- 영화 목록 아이템에 대한 Skeleton UI를 구현한다.
- Skeleton UI는 템플릿으로 제공되는 파일 이외로 자유롭게 구현할 수 있다.

## 검색

- 영화 검색 API를 이용하여 영화를 검색할 수 있다.
  - 엔터키를 눌러 검색할 수 있다.
  - 검색 버튼을 클릭하여 검색할 수 있다.
- 영화 목록 조회와 같이 검색한 결과에 한해 정보를 보여주는 화면의 요구사항은 동일하다.

## 추가 고려사항

- 좌상단 로고 클릭 시 인기있는 영화 페이지로 이동한다.
- 영화 포스터 호버 시 dimmed 처리가 되며, over review 글귀를 출력한다 - (후순위)
- 넷플릭스, 왓챠 type할때마다 밑에 있는 리스트가 re-render (더 후순위)

# 예외 사항
- 인기있는 영화 API 요청을 보냈을 때, 잘못된 응답이 온 경우 error screen을 출력한다.
  - status code 별로 error screen을 다르게 출력한다. (후순위)
- 영화 검색 API 요청을 보냈을 때, 잘못된 응답이 온 경우 error screen을 출력한다.
  - status code 별로 error screen을 다르게 출력한다. (후순위)
- 검색 inputField 제한
  - 최대 입력 길이 30자


## step2

- 영화 상세정보 조회
  - 영화 포스터나 제목을 클릭하면 자세한 예고편이나 줄거리 등의 정보를 보여준다.
  - 상세 정보를 보여주는 모달 창을 구현한다.
  - 키보드의 ESC 키를 누르면 모달 창을 닫을 수 있는 등 사용성을 고려한다.

  - *아래 api 이용*
    - https://developer.themoviedb.org/reference/movie-details 이용

  - 제목, 장르, 별점, 상세, 내 별점


- 별점 매기기
  - 사용자는 영화에 대해 별점을 줄 수 있으며 새로고침하더라도 사용자가 남긴 별점은 유지되어야 한다.
  - 별점은 5개로 구성되어 있으며 한 개당 2점이며 1점 단위는 고려하지 않는다.
    - 2점: 최악이예요
    - 4점: 별로예요
    - 6점: 보통이에요
    - 8점: 재미있어요
    - 10점: 명작이에요

  - UX
    - 현재 별점을 먼저 보여주고, 다른 별에 호버 시 그 점수에 맞도록 변경된다.
    - 클릭 시 오른쪽 점수와 멘트가 변한다.


- UI/UX 개선하기
  - 영화 목록과 영화 상세 정보가 뜨는 모달창에 대한 반응형 레이아웃을 구성한다.

  - breakpoint
    - mobile: 390
    - tablet: 834
    - desktop: 1280

  - 헤더
    - 데스크탑 ~ 태블릿까지는 단순 헤더 간격이 줄어든다.
    - 모바일 화면에는 검색창이 아이콘으로 사라지고, 아이콘을 클릭 시 아래 검색창이 등장한다.

  - MovieItems
    - 데스크탑 column 4
    - 태블릿 column 3
    - 모바일 column 2

  - 모달
    - 데스크탑: 826 * 577
    - 태블릿: 740 * 544
    - 모바일: 100% * 485 

  - 영화 목록에서 더보기 버튼을 눌렀을 때 페이징하는 방식에서 무한 스크롤 방식으로 변경한다.
   - 사용자가 브라우저 화면의 끝에 도달하면 그 다음 20개의 목록을 서버에 요청하여 추가로 불러올 수 있다.
