- Grok Pattern Test Site <br>
1. [Grok Debugger](grokdebug.herokuapp.com/discover?#)<br>
2. [Grok Constructor](grokconstructor.appspot.com/do/match?example=2)<br>
3. Kibana - Dev Tools - Grok Debugger<br>

### gsub 멀티필드 적용
log.file.path, logstash 자동으로 저장되는 필드 중 하나<br>
윈도우의 경우 경로에 '\' 특수문자가 포함되어, ES 저장시 형식이 깨짐 ("""경로""")<br>
gsub을 이용하여 변경해줄 수 있음.<br>

logstash의 멀티필드 문법은 [log][file][path]<br>

```
grok {
  mutate {
    gsub => [
      "[log][file][path]", "\\|\\"", "/"
    ]
  }
}
```
