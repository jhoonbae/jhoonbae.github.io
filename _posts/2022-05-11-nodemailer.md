---
title: “nodemailer으로 메일 발송하기”
categories:
- blogging
last_modified_at: 2022-05-11
toc: true
---

# node.js 에서 mail 발송하기

****

#### nodejs 메일발송
2차 추가 인증을 위해서 otp를 메일로 전송하는 방법을 기록하기 위해 글을 남깁니다.

- **nodemailer**라는 모듈을 사용하면 쉽게 메일을 발송할 수 있습니다.



```
npm i nodemailer
```
모듈을 다운받아줍니다.

```
const nodemailer = require('nodemailer');
require("dotenv").config()
```

모듈을 사용하게 될 라우터에서 호출을 해줍니다.'
환경변수에 id pw를 넣어주고 호출을합니다.

```
        let transporter = nodemailer.createTransport({
            service: "gmail", // 사용할 서비스
            host: 'smtp.gmail.com', 
            port : 587,
            auth: {
                user:process.env.NodeMailer_USER, // id
                pass:process.env.NodeMailer_PASS  // password
            }
        })
```

```
        let mailOption = {
            from : process.env.NodeMailer_USER,
            to : 보내는곳의 이메일,
            subject : '메일 테스트', // 제목
            html: `<p>뭐가 어쩌고 저쩌고<p>`, // 메일안의 내용
        }
        
        transporter.sendMail(mailOption, (error, result) => {
            if(error){
                console.log("Email 발송 에러", error)
                reject({success : false, message : "email 발송 실패"})
            }else{
                console.log("email 발송 성공", result)
                resolve(data)
            }
        })
```

return은 promise객체로 받게 설정을 해놓았기 때문에 resolve, reject 입니다. 필수 아닙니다.

포스트맨으로 요청을 하고 메일을 들어가보면
![](https://velog.velcdn.com/images/baeeunwoo/post/218c3909-3a11-453c-97c9-943716c308d8/image.png)

이렇게 메일이 도착해있는 모습을 볼 수 있습니다.
참고로 gmail  요청시 
535-5.7.8 username and password not accepted.
이렇게 오류가 나는 경우는
 https://myaccount.google.com/lesssecureapps?pli=1 여기에서 설정 변경하면 발송됩니다.
