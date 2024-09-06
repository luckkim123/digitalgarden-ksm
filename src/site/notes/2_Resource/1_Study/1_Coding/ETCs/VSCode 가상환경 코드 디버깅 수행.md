---
{"dg-publish":true,"permalink":"/2-resource/1-study/1-coding/et-cs/vs-code/","tags":["Study/Coding/VSCode"],"noteIcon":"","created":"2024-07-09"}
---

- 실행하고자 하는 코드가 있는 프로젝트 폴더에 `launch.json` 파일 생성
```json title:launch.json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Debug a current file",
            "type": "debugpy",
            "request": "launch",
            "program": "${file}",
            "console": "integratedTerminal",
            "python": "/PATH/TO/YOUR/PYTHON" // which python3.10
        }
    ]
}
```