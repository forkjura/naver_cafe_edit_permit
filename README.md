# naver_cafe_edit_permit

1. [크롬확장](https://chrome.google.com/webstore/detail/user-javascript-and-css/nbhcbdghjpllgmfilhnhkllmkecfmpld) 설치
2. 설치된 크롬확장 우클릭 > options 클릭
3. Add new sites 클릭하여 아래 4개 스크립트 등록
   - 게시물 리스트, url: https://cafe.naver.com/ca-fe/cafes/11262350/members/*
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
