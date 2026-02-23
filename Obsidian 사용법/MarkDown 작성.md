## 1. 마크다운이란?
***
######## [**Markdown**](https://www.markdownguide.org/getting-started/)은 텍스트 기반의 마크업언어로 2004년 존그루버에 의해 만들어졌으며 쉽게 쓰고 읽을 수 있으며 HTML로 변환이 가능하다. 특수기호와 문자를 이용한 매우 간단한 구조의 문법을 사용하여 웹에서도 보다 빠르게 컨텐츠를 작성하고 보다 직관적으로 인식할 수 있다. 마크다운이 최근 각광받기 시작한 이유는 깃헙([https://github.com](https://github.com/)) 덕분이다. [[GitHub]]의 저장소Repository에 관한 정보를 기록하는 README.md는 깃헙을 사용하는 사람이라면 누구나 가장 먼저 접하게 되는 마크다운 문서였다. 마크다운을 통해서 설치방법, 소스코드 설명, 이슈 등을 간단하게 기록하고 가독성을 높일 수 있다는 강점이 부각되면서 점점 여러 곳으로 퍼져가게 된다.


## 2. 마크다운 문법
***
#### 2.1 Header
*****
>
```
# This is a H1
## This is a H2
### This is a H3
#### This is a H4
##### This is a H5
###### This is a H6
```
#### 2.2 BlockQuote
*****
```
> This is a first blockqute.
>	> This is a second blockqute.
>	>	> This is a third blockqute.
```

>This is a first blockqute.
>	>This is a second blockqute.
>	>	>This is a third blockqute.

###### 이 안에서는 다른 마크다운 요소를 포함할 수 있다.

>### This is a H3
>	>- List 
>	>	>code

#### 2.3 코드
*****
###### 2.3.1 들여쓰기 사용(한 줄 띄어쓰기)
This is a normal paragraph:

	This is a code block
	
end code block.

###### 2.3.2 코드 블록
- `<pre><code>{code}</code></pre>` 혹은 ''' 이용

<pre>
<code>
public class BootSpringBootApplication {
  public static void main(String[] args) {
    System.out.println("Hello, Honeymon");
  }

}
</code>
</pre>
```java

public class BootSpringBootApplication {
  public static void main(String[] args) {
    System.out.println("Hello, Honeymon");
  }

}
```

#### 2.4 수평선
***
 ###### 아래 줄은 모두 수평선을 만든다.
 ```
* * *

***

*****

- - -

---------------------------------------
```

#### 2.5 링크
***
###### -2.5.1 참조링크
```
[link keyword][id]

[id]: URL "Optional Title here"

// code
Link: [Google][googlelink]

[googlelink]: https://google.com "Go google"
```
###### -2.5.2 외부링크
```
사용문법: [Title](link)
적용예: [Google](https://google.com, "google link")
```
###### -2.5.3 예시
###### 참조링크 : 
Link: [Google][googlelink]
[googlelink]: https://google.com "Go google"

외부링크 : 
[Google](https://google.com , "google link")

- 2.5.4 자동연결

```
일반적인 URL 혹은 이메일주소인 경우 적절한 형식으로 링크를 형성한다.

* 외부링크: <http://example.com/>
* 이메일링크: <address@example.com>
```

#### 2.6 강조
***
```
*single asterisks*
_single underscores_
**double asterisks**
__double underscores__
~~cancelline~~
```

*single asterisks*
_single underscores_
**double asterisks**
__double underscores__
~~cancelline~~
문장 중간에 사용할 경우에는 **띄어쓰기**를 사용하는 것이 좋다.

#### 2.7 이미지
***
```
![Alt text](/path/to/img.jpg)
![Alt text](/path/to/img.jpg "Optional title")
```

사이즈 조절 기능은 없기 때문에 `<img width="" height=""></img>`를 이용한다.

예

```
<img src="/path/to/img.jpg" width="450px" height="300px" title="px(픽셀) 크기 설정" alt="RubberDuck"></img><br/>
<img src="/path/to/img.jpg" width="40%" height="30%" title="px(픽셀) 크기 설정" alt="RubberDuck"></img>
```

#### 2.8 표
null
|제목|내용|설명|
|------|---|---|
|테스트1|테스트2|테스트3|
|테스트1|테스트2|테스트3|
|테스트1|테스트2|테스트3|

