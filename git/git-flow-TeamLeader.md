# Git flow as a TeamLeader
[๐install git flow HERE](https://danielkummer.github.io/git-flow-cheatsheet/index.html)<br/><br/><br/>

- ๋ค์ด๊ฐ๊ธฐ ์ ์...

  ํ์์ด ํ repo๋ฅผ forkํด์ test.md๋ผ๋ ์์๋ฌผ์ push ํ๋ค. ๊ทธ ๋ค์ ์๊ธฐ repo develop์์ ํ repo develop๋ก request ์์ฒญ์ ํ๋ค. ํ์ฅ์ธ ๋๋ ๊ทธ ์์ฒญ์ mergeํด์ ํ repo develop์๋ test.md๊ฐ ์๋ฐ์ดํธ๋์ง๋ง main์ผ๋ก merge๋ ์ํฉ์ ์๋๋ค.

  ํ์ฅ์ธ ๋๋ ํ์ฌ ํ organization์ fork ํ์ง ์์๊ณ , ํrepo develop์ ์๋ก ์ถ๊ฐ๋ test.md ๋ฅผ main์ mergeํ๊ณ  ์ถ์ ์ํฉ์ด๋ค.<br/><br/>
    <img style="width:500px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FZyFmp%2FbtrHtwjkUlI%2F0wuk62Zmco1K0x3NQ0CAek%2Fimg.png"><br/><br/><br/>

  ๋ฐ๋ก git remote -v ํ์ ๋ origin ํ๋ ๋ฟ์ด๋ฉฐ origin์ ์ฃผ์๋ ํ ์ฃผ์๋ก ๋์ด ์๋ค.<br/><br/>
  <img style="width:500px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbar1kz%2FbtrHqngCmtF%2F4r8WfU9BMdb43Kaz5wOYt0%2Fimg.png"><br/><br/><br/><br/>

## ๋ชฉํ
github main์ test.md ํ์ผ์ ์ฌ๋ฆฌ๊ณ  ์ด๊ฒ์ด ์ฌ๋ผ๊ฐ ๋ฒ์ ์ v0.2๋ก releaseํ์!<br/><br/><br/><br/>

## โก git pull origin develop

  <img style="width:500px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Ft4i7I%2FbtrHwlVIsht%2F3xIlcTqczkO4vHDtuOBDCk%2Fimg.png"><br/><br/>

์ ์ผ ์ฒซ ๋ฒ์งธ ๋จ๊ณ๋ ์ผ๋จ ๋ด local์ ํ repo develop์ ์๋ ์ ๊ท ์ํ๋ฅผ ๋๊ณ  ์ค๋ ๊ฒ.

ํ repo์ develop์ ๋น๊ฒจ์ค์.

๊ทธ๋ฌ๋ฉด ์ ์ฌ์ง์ฒ๋ผ create mode ~~ test.md ๋ผ๊ณ  test.md๋ผ๋ ํ์ผ์ด ๋ง๋ค์ด์ก๋ค๊ณ  ๋ฌ๋ค.

์ด์  ๋ด ๋ก์ปฌ์ ์ต์  ์ํ๋ก ๊ตฌ์ฑ๋๋ค. ์ด๋ ๊ฒ ๋ชจ๋  ๊ฒ์ด ์ต์  ์ํ๋ผ๋ ๊ฒ์ ํ์ธํ๊ณ  release๋ฅผ ํด์ผ ํ๋ค.

์ฃผ์ : main์ด ์๋๋ผ develop ๋ธ๋์น์์ ํํด์ ธ์ผ ํ๋ค.<br/><br/><br/><br/>


## โกโก git flow release start v0.2 

  <img style="width:500px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbtQODt%2FbtrHpPjk61h%2FemSqRRNmEX3CBCkT03Ov20%2Fimg.png"><br/><br/>
version 0.2๋ฅผ release ํ๊ฒ ๋ค๊ณ  ์๋ ฅํ๋ฉด ์์ ๊ฐ์ ๊ธ์ด ๋ฌ๋ค.

- develop์ ๊ธฐ๋ฐ์ผ๋ก release/v0.2๋ผ๋ branch ๋ฅผ ๋ง๋ค์๋ค. (develop ๋ธ๋์น์ ์๋ ๋ด์ฉ๋ค์ ๊ฐ์ ธ์์ ๋ง๋ค์ด์ก๋ค๋ ๋ป์ด๋ค.)

- ์์น๋ develop์์ release/v0.2๋ก ์ด๋๋์๋ค.

- start v0.2๋ฅผ ์คํํ ์๊ฐ๋ถํฐ๋ ์์ ํ  ๊ฒ๋ค์ ์์ ํ๊ณ  ๋ชจ๋  ์ค๋น๊ฐ ๋ค ๋๋๋ฉด git flow release finish v0.2๋ผ๋ ๋์์ ์ํํด๋ผ.

  <img style="width:500px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcap1Sl%2FbtrHpOknmjP%2FzfK41a960tV135M0J4PSTK%2Fimg.png"><br/><br/>

git branch ๋ช๋ น์ด๋ก ํ์ธํด๋ณด๋ฉด ์ค์ ๋ก ๋๋ release/v0.2๋ผ๋ ๊ณณ์ ์์นํ๋ค.

์ด์  main์ผ๋ก ๊ฐ์ ์ด v0.2๋ฅผ ๋น๊ฒจ์ค์.<br/><br/><br/><br/><br/>



## โกโก git merge release/v0.2 

๊ทธ๋ผ ์ด์  main์ผ๋ก ์ด๋ํด์ v0.2 ๋ธ๋์น์ ๋ด์ฉ์ ๋๊ณ  ์จ๋ค.

merge๋ฅผ ํ๊ธฐ ๋๋ฌธ์ ls ๋ช๋ น์ด๋ก ํ์ธํ์ ๋ main์ test.md๋ผ๋ ํ์ผ์ด ์๋กญ๊ฒ ์์ฑ๋ ๊ฑธ ํ์ธํ  ์ ์๋ค. ๋ชจ๋  ๊ฑธ ๋ค ํ์ธํ์ผ๋๊น finish ํ๋ฉด ๋๋ค.<br/><br/>


โ ์ฌ์ค ์ด ๋จ๊ณ์ ๋ํด์๋ ํ์ ์ด ์๋ค. main์ผ๋ก ์ด๋ํด์ release/v0.2๋ฅผ ๋จธ์ง ํด์ค๋ ํ๋์ release finish ํ๊ธฐ ์ ์ ํด์ผ ํ๋ ๋์์ธ๊ฐ? ์๋ฌธ์ด ๋ ๋ค. ์๋ํ๋ฉด ๋ฐ์์ git flow release finish v0.2๋ฅผ ํ๋ฉด main ๋ธ๋์น๋ก ๋จธ์ง ๋๋ค๋ ๋ฌธ๊ตฌ๊ฐ ๋จ๊ธฐ ๋๋ฌธ์ด๋ค. ๋ค์์ ๋ค์ ํ๋ฒ release๋ฅผ ํด์ ์ด ๋์์ด ํ์คํ ํ์ํ์ง ํ์ธํด์ผ๊ฒ ๋ค.<br/><br/><br/><br/><br/>


## โกโก git flow release finish v0.2

  <img style="width:500px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FoyUmM%2FbtrHrNFTemo%2FmEEIsNQ5HxtLvr0nH2Dxr1%2Fimg.png"><br/>

๊ทธ๋ผ ์ด๋ ๊ฒ tag ๋ฅผ ์จ๋ฌ๋ผ๋ vi(?)๊ฐ ์ด๋ฆฐ๋ค. ๋์ ๊ฒฝ์ฐ v0.2๋ผ๊ณ  ์ ์ฅํ๊ณ  ๋์๋ค.<br/><br/><br/><br/>

  <img style="width:500px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FDYuAa%2FbtrHsDXocnf%2FIYpFeG23nJ3EYIPXYU6Sn1%2Fimg.png"><br/>

์ ๋ฌ๊ณ  ๋์ค๋ฉด ์ด์  git push ํด์ ๋ก์ปฌ์ ์ปค๋ฐ ํด๋ผ, main์ผ๋ก ๋จธ์ง๊ฐ ๋๋ค, tag๋ 0.2๋ก ๋์๋ค. ๊ทธ๋ฆฌ๊ณ  ์ด์  ๋ ์ด์ ํ์ ์๋ ๋ธ๋์น release/v0.2๋ฅผ ์ญ์ ํ๋ค. ๊ทธ๋ฆฌ๊ณ  ๋ด ์์น๋ main์ ์๋ค.๋ผ๋ ๋ฌธ๊ตฌ๊ฐ ๋ฌ๋ค.<br/>

git branch๋ก ํ์ธํด๋ณด๋๊น ์ค์ ๋ก ๋ main์ ์๊ณ  release/v0.2๋ ์์ด์ก๋ค.<br/><br/>

- release/v0.2๊ฐ main์ผ๋ก ๋จธ์ง ๋๋ค.
- 0.2๋ก ํ๊ทธ ๋์๋ค.
- release/v0.2๊ฐ ์ญ์ ๋์๋ค.
- ์์น๊ฐ main์ผ๋ก ์ด๋๋์๋ค.
  
  (release finish์ ์ฒซ ๋ฒ์งธ์ ๋ค ๋ฒ์งธ ์ญํ ์ ๋ดค์ ๋, ์์  ๋จ๊ณ์์ ๊ตณ์ด main์ผ๋ก ๊ฐ์ release/v0.2 ๋ฅผ mergeํ์ง ์์๋ ๋๋ ๊ฑฐ ์๋๊ฐ? ๋ผ๋ ์์ฌ์ด ๋ค์๋ค.)<br/><br/><br/><br/><br/>


## โก git push --tags

  <img style="width:500px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbTkxhM%2FbtrHvoLVL90%2F3AKgQyusaHrqwZRPOVWWO0%2Fimg.png"><br/><br/>

์ฌ๊ธฐ์ ์ฃผ์ํด์ผ ํ๋ ๊ฒ์ด. git push origin main์ ํ๊ธฐ ์ ์ tag๋ฅผ pushํด์ผ ํ๋ค. ๋ง ๊ทธ๋๋ก tag๋ฅผ remote์ push ํ๋ ๋ช๋ น์ด๋ค.

์ด ๋จ๊ณ๋ฅผ ๋จผ์  ๊ฑฐ์น๋ ์ด์ ๋ ์ฐ๋ฆฌ๋ v0.2๋ผ๋ tag์ ์๋ก ๋ฐ๋ ๋ฒ์ ์ ๋ฃ์ด์ผ ํ๊ธฐ ๋๋ฌธ์ด๋ค.<br/><br/><br/><br/><br/>


## โก git push origin main
  <img style="width:500px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbhiYAT%2FbtrHunfrYaT%2FTxgs6ic1eMNs3fEyhx7Mz1%2Fimg.png"><br/>

๊นํ main์๋ค๊ฐ push ํ๊ธฐ๋ง ํ๋ฉด release ์์ ์๋ฃ. ๊ทธ๋ผ github team repo๋ก ๋์๊ฐ ์ ๋๋ก test.md ๊ฐ v0.2์ ์ ์ฌ๋ผ์๋ ํ์ธํด๋ณด์.<br/><br/><br/>

  <img style="width:500px" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbkQLKU%2FbtrHtvSkIo1%2FjInO5cdWXZXRj6k2VTl8Ak%2Fimg.png"><br/>

ํ์ธํด๋ณด๋ฉด main์ test.md ํ์ผ์ด ์ ๋๋ก ๋ค์ด์จ ๊ฑธ ํ์ธํ  ์ ์๋ค.

release ๋!<br/><br/><br/>


## ๋๋ ์ 
์ ์๋ ํ์์ผ๋ก ์ฐธ์ฌํด์ git flow release ๋ผ๋ ์์์ ์ง์  ๊ฒฝํํ  ๊ธฐํ๊ฐ ์์๋๋ฐ, ์ด๋ฒ์ ์คํฐ๋ ์กฐ์๋ค๊ณผ ํจ๊ป ์๋ก์ด organization์ ๋ง๋ค์ด release๋ฅผ ์ง์  ๊ฒฝํํ๊ฒ ๋๋ค. ๋ด๊ฐ release์ ๋ํ ๊ฒฝํ๊ณผ ์ดํด๊ฐ ๋ถ์กฑํ ์ํฉ์์ ์กฐ์๋ค๊ณผ release ํ๋ ๋ฐ๋์ ์ดํด๊ฐ ์ถฉ๋ถํ ๋์ง ์์ ์ํฉ์์ ๋ช๋ น์ด๋ฅผ ์ด ์ ์ด ์์ฝ๋ค. ๊ทผ๋ฐ TIL ์ฐ๋ฉด์ ๋ค์ ์ ๋ฆฌํด ๋ณด๋ ์ ์ด๋ฐ ์ ์ฐจ๋ฅผ ๋ฐ์๋์ง ์ดํด๊ฐ ๋๋ค.

release ๊ณผ์  ์ค์ main์์ release/v0.2๋ฅผ merge ํ๋ ๋จ๊ณ๊ฐ ์๋๋ฐ, ์ด ๋ถ๋ถ์ด ์ข ํท๊ฐ๋ ธ๋ค. release๋ฅผ ๋จผ์  ํด๋ณธ ์กฐ์๋ค์ด ์ ์ ์ด ๊ณผ์ ์์ ์ค๋ฅ๊ฐ ์์๋๋ฐ ๊ทธ๊ฑธ ํด๊ฒฐํ๋ ๋ฐฉ๋ฒ์ด main์ผ๋ก ๊ฐ์ release/v0.2 ๋ฅผ mergeํ๋ ๊ฒ์ด์๋ค๊ณ  ํด์ ํ๋๋ฐ, ๊ฒฐ๊ณผ์ ์ผ๋ก ์ค๋ฅ๋ ๊ฑด ์์๋ค.

๊ทผ๋ฐ TIL์ ์ฐ๋ฉด์ ๋ณด๋๊น git flow release finish v0.2๋ผ๋ ๋ช๋ น์ด๋ฅผ ์ฐ๋ฉด ์์น๋ฅผ main์ผ๋ก ์ด๋์์ผ์ release/v0.2๋ฅผ merge ํด์ค๋๋ฐ ๊ตณ์ด ์์์ merge๋ฅผ ํด์ค ํ์๊ฐ ์์์๊น? ์๋ฌธ์ด ๋ค์๋ค. ๋ค์์ release ํ  ๋๋ ๊ทธ ๋จ๊ณ๋ฅผ ๋ฐ์ด ๋๊ณ  ๋ฐ๋ก release finish๋ฅผ ์๋ํด๋ด์ผ๊ฒ ๋ค.<br/><br/>

2022.07.17







