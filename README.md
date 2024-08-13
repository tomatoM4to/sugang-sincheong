# sugang-sincheong
```js
async function AutoLogin(hours) {
    async function getTime(url) {
        try {
            const response = await fetch(url, {
                method: 'get',
                mode: 'no-cors'
            });

            let date = response.headers.get('Date');
            return new Date(date);

        } catch (error) {
            console.error('서버 시간을 가져오는 데 실패했습니다. 함수를 종료 합니다.');
            return null;
        }
    }

    let loginButton = document.querySelector('#button_login');
    if (!loginButton) {
        throw new Error('로그인 버튼을 찾을 수 없습니다.');
    }

    while (true) {
        let serverTime = await getTime('https://sugang.kangwon.ac.kr/login/loginPage.do');

        if (!serverTime) break;

        // 오전 10시 이상인지 확인
        if (serverTime.getHours() >= hours) {
            let loginButton = document.querySelector('#button_login');
            loginButton.click();
            break;
        } else {
            console.log(`아직 ${hours}시가 되지 않았습니다. 기다리는 중...`);
        }
    }
}
AutoLogin(10);
```
