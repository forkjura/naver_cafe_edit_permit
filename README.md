# naver_cafe_edit_permit

1. [크롬확장](https://chrome.google.com/webstore/detail/user-javascript-and-css/nbhcbdghjpllgmfilhnhkllmkecfmpld) 설치
2. 설치된 크롬확장 페이지 진입, 링크: chrome-extension://nbhcbdghjpllgmfilhnhkllmkecfmpld/options.html
3. Add new sites 클릭하여 본 글 최하단 4개 스크립트 등록
4. 디매 홈 > 나의활동 > '내가쓴 게시글' 우클릭
5. 가장 오래된 게시물 페이지(끝페이지)로 이동 후 '페이지 이동시마다 여기를 눌러요' 를 클릭하면 자동진행
6. 한페이지 자동작업 끝나면 한페이지 이동 후 '페이지 이동시마다 여기를 눌러요' 클릭 반복
7. 모든 페이지 작업 완료되면 크롬확장을 지우거나 설정 페이지에서 전체 스크립트 비활성화

- 스크립트1: 게시물 리스트, url: https://cafe.naver.com/ca-fe/cafes/11262350/members/*
- ```Javascript
     function removeLink(event) {
          setTimeout(function() {
              link.remove(); 
          }, 500);
      }
      
      function chk(){
      	if(document.getElementsByClassName('profile_info_area')[0]){
      		var button = document.createElement('button');
      		button.textContent = '페이지 이동시마다 여기를 눌러요';
      		button.style.color = 'blue';
      		document.getElementsByClassName('profile_info_area')[0].appendChild(button);
      		// 버튼 클릭 이벤트 핸들러를 연결합니다.
      		button.addEventListener('click', function () {
      		    var articleLinks = document.querySelectorAll('a.article');
      		    for (var i = 0; i < articleLinks.length; i++) {
      		        articleLinks[i].addEventListener('click', removeLink);
      		    }
      		});
      	}else{
      		setTimeout(chk, 200);
      	}
      }
      chk()
     ```
- 스크립트2: 수정완료창, url: https://cafe.naver.com/dieselmania/4
- ```Javascript
  setTimeout(function() {
	   window.close()
   }, 500);  
  ```
- 스크립트3: 수정창, url: https://cafe.naver.com/ca-fe/cafes/11262350/articles/*
- ```Javascript
  function chk(){
  var btn = document.getElementsByClassName('BaseButton BaseButton--skinGreen size_default')
  if (btn[0]
  && document.getElementsByClassName('btn_open_set')[0]
  && document.getElementById('member')
  && document.getElementById('permit')
  && document.getElementsByClassName('textarea_input')[0]
  && document.getElementsByClassName('textarea_input')[0].value!=''){
  	var c = document.getElementsByClassName('open_select')[1].innerText.includes('비공')
  	document.getElementsByClassName('btn_open_set')[0].click()
  	document.getElementById('member').click()
    if(c){
       document.getElementById('permit').click()
    }
    window.addEventListener("beforeunload", function (event) {
        window.close()
        closeWindow();
    });
    setTimeout(function() {
       document.getElementsByClassName('BaseButton BaseButton--skinGreen size_default')[0].click()
    }, 500);
       
    }else{
       setTimeout(chk, 200);
    }
 	}
 	chk()
  ```
- 스크립트4: 게시물창, url: https://cafe.naver.com/dieselmania?iframe_url_utf8=%2FArticleRead.nhn*
- ```Javacript
  function chk(){
	if(
		document.getElementById('cafe_main')
		&& document.getElementById('cafe_main').contentWindow.document
		&& document.getElementById('cafe_main').contentWindow.document.getElementsByClassName("left_area")[0]
		&& document.getElementById('cafe_main').contentWindow.document.getElementsByClassName("left_area")[0].children[0]
		){
			document.getElementById('cafe_main').contentWindow.document.getElementsByClassName("left_area")[0].children[0].click()
			setTimeout(function() {window.close()}, 500);
		}
	else{
		setTimeout(chk,300)
	}
   }
   chk()
  ```
