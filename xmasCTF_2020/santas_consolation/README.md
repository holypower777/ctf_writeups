# Santa's consolation (500 points)

## Description

Santa's been sending his regards; he would like to know who will still want to hack stuff after his CTF is over.

Note: Bluuk is a multilingual bug bounty platform that will launch soon and we've prepared a challenge for you. Subscribe and stay tuned!

Target: https://bluuk.io

Author: littlewho

## Solution

```javascript
console.log("🐢 Javascript Challenge 🐢");
console.log("Call win(<string>) with the correct parameter to get the flag");
console.log("And don't forget to subscribe to our newsletter :D");

function check(s) {
    const k = "MkVUTThoak44TlROOGR6TThaak44TlROOGR6TThWRE14d0hPMnczTTF3M056d25OMnczTTF3M056d1hPNXdITzJ3M00xdzNOenduTjJ3M00xdzNOendYTndFRGY0WURmelVEZjNNRGYyWURmelVEZjNNRGYwRVRNOGhqTjhOVE44ZHpNOFpqTjhOVE44ZHpNOEZETXh3SE8ydzNNMXczTnp3bk4ydzNNMXczTnp3bk13RURmNFlEZnpVRGYzTURmMllEZnpVRGYzTURmeUlUTThoak44TlROOGR6TThaak44TlROOGR6TThCVE14d0hPMnczTTF3M056d25OMnczTTF3M056dzNOeEVEZjRZRGZ6VURmM01EZjJZRGZ6VURmM01EZjFBVE04aGpOOE5UTjhkek04WmpOOE5UTjhkek04bFRPOGhqTjhOVE44ZHpNOFpqTjhOVE44ZHpNOGRUTzhoak44TlROOGR6TThaak44TlROOGR6TThSVE14d0hPMnczTTF3M056d25OMnczTTF3M056d1hPNXdITzJ3M00xdzNOenduTjJ3M00xdzNOenduTXlFRGY0WURmelVEZjNNRGYyWURmelVEZjNNRGYzRVRNOGhqTjhOVE44ZHpNOFpqTjhOVE44ZHpNOGhETjhoak44TlROOGR6TThaak44TlROOGR6TThGak14d0hPMnczTTF3M056d25OMnczTTF3M056d25NeUVEZjRZRGZ6VURmM01EZjJZRGZ6VURmM01EZjFFVE04aGpOOE5UTjhkek04WmpOOE5UTjhkek04RkRNeHdITzJ3M00xdzNOenduTjJ3M00xdzNOendITndFRGY0WURmelVEZjNNRGYyWURmelVEZjNNRGYxRVRNOGhqTjhOVE44ZHpNOFpqTjhOVE44ZHpNOFZETXh3SE8ydzNNMXczTnp3bk4ydzNNMXczTnp3WE94RURmNFlEZnpVRGYzTURmMllEZnpVRGYzTURmeUlUTThoak44TlROOGR6TThaak44TlROOGR6TThkVE84aGpOOE5UTjhkek04WmpOOE5UTjhkek04WlRNeHdITzJ3M00xdzNOenduTjJ3M00xdzNOendITXhFRGY0WURmelVEZjNNRGYyWURmelVEZjNNRGYza0RmNFlEZnpVRGYzTURmMllEZnpVRGYzTURmMUVUTTAwMDBERVRDQURFUg==";
    const k1 = atob(k).split('').reverse().join('');
    return bobify(s) === k1;
}

function bobify(s) {
    if (~s.indexOf('a') || ~s.indexOf('t') || ~s.indexOf('e') || ~s.indexOf('i') || ~s.indexOf('z')) return "[REDACTED]";
    const s1 = s.replace(/4/g, 'a').replace(/3/g, 'e').replace(/1/g, 'i').replace(/7/g, 't').replace(/_/g, 'z').split('').join('[]');
    const s2 = encodeURI(s1).split('').map(c => c.charCodeAt(0)).join('|');
    const s3 = btoa("D@\xc0\t1\x03\xd3M4" + s2);
    return s3;
}

function win(x) {
    return check(x) ? "X-MAS{" + x + "}" : "[REDACTED]";
}
```

We need to decode "k" from base64 and reverse. Then I decided to decode the resulting string from base64 again:

```text
D@À	1.ÓM4115|37|53|66|37|53|68|97|37|53|66|37|53|68|110|37|53|66|37|53|68|116|37|53|66|37|53|68|97|37|53|66|37|53|68|122|37|53|66|37|53|68|119|37|53|66|37|53|68|105|37|53|66|37|53|68|115|37|53|66|37|53|68|104|37|53|66|37|53|68|101|37|53|66|37|53|68|115|37|53|66|37|53|68|122|37|53|66|37|53|68|121|37|53|66|37|53|68|48|37|53|66|37|53|68|117|37|53|66|37|53|68|122|37|53|66|37|53|68|99|37|53|66|37|53|68|114|37|53|66|37|53|68|97|37|53|66|37|53|68|99|37|53|66|37|53|68|105|37|53|66|37|53|68|117|37|53|66|37|53|68|110|37|53|66|37|53|68|122|37|53|66|37|53|68|102|37|53|66|37|53|68|101|37|53|66|37|53|68|114|37|53|66|37|53|68|105|37|53|66|37|53|68|99|37|53|66|37|53|68|105|37|53|66|37|53|68|116
```

Then i decoded it from decimal:

```text
s%5B%5Da%5B%5Dn%5B%5Dt%5B%5Da%5B%5Dz%5B%5Dw%5B%5Di%5B%5Ds%5B%5Dh%5B%5De%5B%5Ds%5B%5Dz%5B%5Dy%5B%5D0%5B%5Du%5B%5Dz%5B%5Dc%5B%5Dr%5B%5Da%5B%5Dc%5B%5Di%5B%5Du%5B%5Dn%5B%5Dz%5B%5Df%5B%5De%5B%5Dr%5B%5Di%5B%5Dc%5B%5Di%5B%5Dt
```

And url decode for now:

```text
s[]a[]n[]t[]a[]z[]w[]i[]s[]h[]e[]s[]z[]y[]0[]u[]z[]c[]r[]a[]c[]i[]u[]n[]z[]f[]e[]r[]i[]c[]i[]t
```

So, lets get rid of unnecessary symbols ("[" and "]"), then change some symbols which are specified in the function **bobify** and provide it to win function to check whether the flag is true:

```text
s4n74_w1sh3s_y0u_cr4c1un_f3r1c17
```

Flag: X-MAS{s4n74_w1sh3s_y0u_cr4c1un_f3r1c17}