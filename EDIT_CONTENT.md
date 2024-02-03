# naver_cafe_edit_permit

1. [크롬확장](https://chrome.google.com/webstore/detail/user-javascript-and-css/nbhcbdghjpllgmfilhnhkllmkecfmpld) 설치
2. 설치된 크롬확장 페이지 진입, 링크: chrome-extension://nbhcbdghjpllgmfilhnhkllmkecfmpld/options.html
3. Add new sites 클릭하여 본 글 최하단 4개 스크립트 등록
4. 디매 홈 > 나의활동 > '내가쓴 게시글' 우클릭
5. 가장 오래된 게시물 페이지(끝페이지)로 이동 후 '페이지 이동시마다 여기를 눌러요' 를 클릭하면 자동진행
6. 한페이지 자동작업 끝나면 한페이지 이동 후 '페이지 이동시마다 여기를 눌러요' 클릭 반복
7. 모든 페이지 작업 완료되면 크롬확장을 지우거나 설정 페이지에서 전체 스크립트 비활성화

- 스크립트1: 게시물 리스트, url: [https://cafe.naver.com/ca-fe/cafes/11262350/members/*](https://cafe.naver.com/ca-fe/cafes/11262350/members/.*)
- ```Javascript
     // Here You can type your custom JavaScript...
     function aClick(){
   	if(document.getElementsByClassName('article')[0]){
   	  if(document.getElementsByClassName('article')[0].innerText.includes('월')){
   	    setTimeout(function() {
     			document.getElementsByClassName('article')[0].remove()
     		}, 300);
     		setTimeout(aClick, 800)
     		return
   	  }
   		document.getElementsByClassName('article')[0].click()
   		setTimeout(function() {
   			document.getElementsByClassName('article')[0].remove()
   		}, 300);
   		setTimeout(aClick, 4500)
   	}
   }
    
    function chk(){
    	if(document.getElementsByClassName('profile_info_area')[0]){
    		var button = document.createElement('button');
    		button.textContent = '페이지 이동시마다 여기를 눌러요';
    		button.style.color = 'blue';
    		document.getElementsByClassName('profile_info_area')[0].appendChild(button);
    		// 버튼 클릭 이벤트 핸들러를 연결합니다.
    		button.addEventListener('click', function () {
    		    aClick()
    		});
    	}else{
    		setTimeout(chk, 200);
    	}
    }
    chk()
  ```
- 스크립트2: 수정창, url: .*ArticleRead\.nhn.*
- ```Javascript
  // Here You can type your custom JavaScript...
  function chk(){
    if(
    	document.getElementById('cafe_main')
    	&& document.getElementById('cafe_main').contentWindow.document
    	&& document.getElementById('cafe_main').contentWindow.document.getElementsByClassName("left_area")[0]
    	&& document.getElementById('cafe_main').contentWindow.document.getElementsByClassName("left_area")[0].children[0]
    	){
    		document.getElementById('cafe_main').contentWindow.document.getElementsByClassName("left_area")[0].children[0].click()
    		//setTimeout(function() {window.close()}, 500);
    		setTimeout(chk2, 500);
    	}
    else{
    	setTimeout(chk,300)
    }
   }
  chk()
  
  function chk2() {
      if (document.getElementById('cafe_main') && document.getElementById('cafe_main').contentWindow.document.querySelector('iframe[title="글쓰기영역"]')) {
          var djcaf = document.getElementById('cafe_main').contentWindow.document;
          var djdoc = djcaf.querySelector('iframe[title="글쓰기영역"]').contentWindow.document;
          var boldTags = djdoc.getElementsByTagName('b');
          for (var i = 0; i < boldTags.length; i++) {
              var content = boldTags[i].textContent || boldTags[i].innerText;
              if (content.startsWith("📢 New! 로또")) {
                  boldTags[i].parentElement.parentElement.remove(boldTags[i].parentElement);
                  djcaf.getElementById('cafewritebtn').click();
                  setTimeout(chk3, 500);
                  break;
              }
          }
          setTimeout(chk2, 500);
          //setTimeout(function() {window.close()}, 5000);
          /*window.addEventListener("load", function(event) {
              window.close()
              closeWindow();
          });*/
      } else {
          setTimeout(chk2, 200);
      }
  }
  
  function chk3(){
    if(
    	document.getElementById('cafe_main')
    	&& document.getElementById('cafe_main').contentWindow.document
    	&& document.getElementById('cafe_main').contentWindow.document.getElementsByClassName("left_area")[0]
    	&& document.getElementById('cafe_main').contentWindow.document.getElementsByClassName("left_area")[0].children[0]
    	){
    		//window.close();
    		//setTimeout(window.close, 1);
    		setTimeout(function() {window.close()}, 500);
    	}
    else{
    	setTimeout(chk3,300);
    }
   }
  ```
