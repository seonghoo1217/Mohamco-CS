# ๐ต GET, POST Method

## HTTP Method

์น์์์ ํด๋ผ์ด์ธํธ๊ฐ ํ๋กํ ์ฝ์ ํตํด ์๋ฒ์ ๋ฐ์ดํฐ๋ฅผ ์์ฒญ(Request)ํ๋ฉด ์๋ฒ๋ ์ด๋ฅผ ์ฒ๋ฆฌํ์ฌ ๊ฒฐ๊ณผ๋ฅผ ํด๋ผ์ด์ธํธ์ ์๋ต(Response)ํด์ฃผ๋๋ฐ ์ด๋, ํด๋ผ์ด์ธํธ๊ฐ ์๋ฒ์๊ฒ ์์ฒญํ๋ ๋ฐฉ๋ฒ์ <span style="color: red">`HTTP Method`</span>๋ผ๊ณ  ํ๋ค. <span style="color: red">`HTTP Method`</span>์๋ 8๊ฐ์ง์ ์ข๋ฅ ์ค ๊ฐ์ฅ ๋ง์ด ์ฐ์ด๋ GET์ POST ๋ฐฉ์์ ์๊ฐํ๊ณ ์ ํ๋ค.
<br>

## GET

> <span style="color: red">`GET`</span> ๋ฐฉ์์ ํด๋ผ์ด์ธํธ๊ฐ ์๋ฒ์๊ฒ ์ด๋ค ๋ฆฌ์์ค๋ฅผ ์์ฒญํ๋ ๊ฒ์ด๋ค.

- `GET`์ HTML ํ์ด์ง๋ฅผ ์์ฒญํ๊ฑฐ๋ ์ด๋ค API๋ฅผ ํตํ์ฌ ๋ฐ์ดํฐ๋ฅผ ์ฝ์ด๋ค์ด๊ฑฐ๋, ์ด๋ฏธ์ง๋ฅผ ๋ก๋ฉํ๊ธฐ ์ํ์ฌ ์์ฃผ ์ฌ์ฉ๋๋ ๋ฉ์๋์ด๋ค. ์ฆ, ๋ฐ์ดํฐ๋ฅผ ๋ฐ์์ค๋ ์ญํ ๋ง ์ํํ๋ค.
- QueryString์ ํ์ฉํด์ ๋ฐ์ดํฐ๋ฅผ ์์ฒญํ๋ฉฐ, **๋ณด์์ ์์ฃผ ์ทจ์ฝํ๋ค.**
- ๋ํ์ ์ธ ํน์ง์ผ๋ก URL์ ํ๋ผ๋ฏธํฐ(Parameter)๋ฅผ ๋ถ์ฌ์ ์ ์กํ๊ธฐ ๋๋ฌธ์ body ์์ญ์ ์ฌ์ฉํ์ง ์๋๋ค.
  - URL ๋ค์ `?`๋ฅผ ์ฌ์ฉํ์ฌ ํ๋ผ๋ฏธํฐ๋ฅผ ์์ฑํ๊ฒ ๋๊ณ  `&`๋ฅผ ๋ถ์ฌ ์ฌ๋ฌ ๊ฐ์ ํ๋ผ๋ฏธํฐ๋ฅผ ๊ตฌ๋ถํ๊ฒ ๋๋ค.
- ํ๋ฒ ์์ฒญ ์ URL ํฌํจ 255์๊น์ง ์ ์ก์ด ๊ฐ๋ฅํ๊ณ , HTTP/1.1์์๋ 2048์๊น์ง ๊ฐ๋ฅํ๋ค.
  <br>

## POST

> <span style="color: red">`POST`</span> ๋ฐฉ์์ ํด๋ผ์ด์ธํธ๊ฐ ์๋ฒ๋ก ๋ฐ์ดํฐ๋ฅผ ๋ณด๋ด๊ณ , ์๋ฒ๊ฐ ์ด ๋ฐ์ดํฐ๋ฅผ ์ฒ๋ฆฌํด ๋ฌ๋ผ๊ณ  ์์ฒญํ๋ ๊ฒ์ด๋ค.

- `POST`๋ ์์ฑ ๋ฐ ์๋ฐ์ดํธ๋ฅผ ํ๊ธฐ ์ํด ์๋ฒ๋ก ๋ฐ์ดํฐ๋ฅผ ๋ณด๋ด๋ ๋ฐ ์ฌ์ฉ๋๋ค. ์ฆ, ์๋ฒ์ ๋ด๊ฐ ์์ฒญํ ๋ฐ์ดํฐ๋ฅผ ์ถ๊ฐ๋ก ์์ํ๊ธฐ ์ํ  ๋ ์ฌ์ฉํ๋ ๋ฉ์๋๋ค.
- ๋ฉ์์ง๋ฅผ ์ ์กํ๊ฑฐ๋, ์ ๊ท ๋ฆฌ์์ค๋ฅผ ์์ฑํ๊ฑฐ๋ ํด๋ผ์ด์ธํธ์ ์๋ ฅ๋ ๋ฐ์ดํฐ๋ฅผ ์ฒ๋ฆฌํ๋ ํ๋ก์ธ์ค๋ฅผ ์๋ฒ ์ธก์์ ์คํํ๊ธฐ ์ํด ์์ฃผ ์ฌ์ฉ๋๋ค.
- ๋ํ์ ์ธ ํน์ง์ผ๋ก `GET`๋ฐฉ์๊ณผ ๋ฌ๋ฆฌ body ์์ญ์ ๋ฐ์ดํฐ๋ฅผ ์ค์ด ๋ณด๋ด ๋ณด์์ด ํ์ํ ๋ถ๋ถ์ ์์ฃผ ์ฌ์ฉ๋๋ค. - body์ ๋ฐ์ดํฐ๋ฅผ ์ค์ด ๋ณด๋ด๊ธฐ ๋๋ฌธ์ ๋ฐ์ดํฐ ์ ์ก์์๋ **๊ธธ์ด ์ ํ์ด ์์ด** ์ฉ๋์ด ํฐ ๋ฐ์ดํฐ๋ฅผ ๋ณด๋ด๋๋ฐ ์ ํฉํ๋ค.
  <br><br>

## GET๊ณผ POST์ ์ฐจ์ด์ 

1. <span style="background-color: #ffd33d">**์ฌ์ฉ์ฉ๋**</span>
   - `GET`์ ์ฌ์ฉ์์๊ฒ ํ์ํ ๋ฐ์ดํฐ๋ฅผ ๋ฐ์์ค๋ ์ญํ ์ ํ๊ณ , `POST`๋ ์ฌ์ฉ์์ ์ด๋ค ํ๋์ ์๋ฒ์ ๋ฐ์ํ๋ ์ญํ ์ ํ๋ค.
   - DB๋ก ์์๋ฅผ ๋ค๋ฉด,`GET`</span>์ SELECT์ ๊ฐ๊น๊ณ ,`POST`๋ CREATE์ ๊ฐ๊น๋ค๊ณ  ๋ณผ ์ ์๋ค.
2. <span style="background-color: #ffd33d">**์บ์ฑ**</span>
   - `GET`์ ํ๋ผ๋ฏธํฐ๋ค์ URL์ ์ผ๋ถ๋ถ์ด๊ธฐ ๋๋ฌธ์ ๋ธ๋ผ์ฐ์  ํ์คํ ๋ฆฌ์ ๋จ๊ฒ๋๊ณ , `POST`๋ ๋ธ๋ผ์ฐ์ ์ ๊ธฐ๋ก์ด ๋จ์ง ์๋๋ค.
   - `GET`์ URL๋ก ์ธ์ฝ๋ฉ๋์ด ์ฆ๊ฒจ์ฐพ๊ธฐ๊ฐ ๊ฐ๋ฅํ๊ณ , `POST`๋ ์ฆ๊ฒจ์ฐพ๊ธฐ๊ฐ ๋ถ๊ฐ๋ฅํ๋ค.
3. <span style="background-color: #ffd33d">**๋ณด์**</span>
   - `GET`์ URL์ ํตํด ๋ชจ๋  ํ๋ผ๋ฏธํฐ๋ฅผ ์ ๋ฌํ๊ธฐ ๋๋ฌธ์ ์ฃผ์์ฐฝ์ ์ ๋ฌ ๊ฐ์ด ๋ธ์ถ๋์ด ๋ณด์์ ์ทจ์ฝํ๊ณ , `POST`๋ ๋ฐ์ดํฐ๊ฐ ๋ธ์ถ๋์ง ์๊ธฐ ๋๋ฌธ์ ๋ณด์์ด ํ์ํ ๊ฒฝ์ฐ์ ์ฉ์ดํ๋ค.
4. <span style="background-color: #ffd33d">**๋ฐ์ดํฐ์**</span>
   - `GET`์ URL ๊ธธ์ด๊ฐ ์ ํ์ด ์์ด ์ ์ก ๋ฐ์ดํฐ์์ด ํ์ ๋์ด ์๊ณ , `POST`๋ ์ ์ก ๋ฐ์ดํฐ์ ์ ํ์ด ์๋ค.
5. <span style="background-color: #ffd33d">**๋ณด์**</span>
   - `GET`์ URL ๊ธธ์ด๊ฐ ์ ํ์ด ์์ด ์ ์ก ๋ฐ์ดํฐ์์ด ํ์ ๋์ด ์๊ณ , `POST`๋ ์ ์ก ๋ฐ์ดํฐ์ ์ ํ์ด ์๋ค.

<br>

## ๋์ ์๊ฒฌ

`GET`๊ณผ `POST`๋ ๋ ๋ค HTTP ํ๋กํ ์ฝ์ ์ด์ฉํด ์๋ฒ์ ๋ฌด์ธ๊ฐ `request`ํ  ๋ ์ฌ์ฉํ๋ ๋ฐฉ์์ด์ง๋ง, ์ฌ์ฉํ๋ ์ํฉ์ด ๋ค๋ฅด๋ค๋ ๊ฒ์ ์ ์ ์๋ค. ์ฆ, <span style="background: #f1f8ff">๊ฐ์ ธ์ฌ ๋์ ์ํํ  ๋๋ฅผ ํ์ํด์ ์ ํฉํ ๊ณณ์ ํ์ฉํด์ผ ํ๋ค. </span>

<br>
 
