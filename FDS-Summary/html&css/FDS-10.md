[1]+  Done                    npm install node-sass
gose:~ $ node-sass -v
node-sass	4.5.2	(Wrapper)	[JavaScript]
libsass  	3.5.0.beta.2	(Sass Compiler)	[C/C++]
gose:~ $ cd FDS04
gose:~/FDS04 (4th_school) $ cd project
gose:~/FDS04/project (4th_school) $ ls
css		flex2.html	index2.html	position.html	transform.html
cube.html	images		ir-sprite.html	tab-ui.html
flex.html	index.html	js		template.html
gose:~/FDS04/project (4th_school) $ mkdir sass
gose:~/FDS04/project (4th_school) $ ls
css		flex2.html	index2.html	position.html	template.html
cube.html	images		ir-sprite.html	sass		transform.html
flex.html	index.html	js		tab-ui.html
gose:~/FDS04/project (4th_school) $ touch sass/test.scss
gose:~/FDS04/project (4th_school) $ node-sass sass/test.scss -o css/
Rendering Complete, saving .css file...
Wrote CSS to /Users/gose/FDS04/project/css/test.css
gose:~/FDS04/project (4th_school) $ cat css/test.css
html {
  font-size: 10px; }

body {
  font-size: 1.4rem;
  color: #181818; }

a {
  color: #181818; }
gose:~/FDS04/project (4th_school) $ node-sass sass/test.sass -o css/
No input file was found.
gose:~/FDS04/project (4th_school) $ node-sass sass/test.scss -o css/
{
  "status": 1,
  "file": "/Users/gose/FDS04/project/sass/test.scss",
  "line": 2,
  "column": 1,
  "message": "Invalid CSS after \"html\": expected 1 selector or at-rule, was \"{\"",
  "formatted": "Error: Invalid CSS after \"html\": expected 1 selector or at-rule, was \"{\"\n        on line 2 of sass/test.scss\n>> html{\n   ^\n"
}
gose:~/FDS04/project (4th_school) $ node-sass sass/test.scss -o css/
Rendering Complete, saving .css file...
Wrote CSS to /Users/gose/FDS04/project/css/test.css
gose:~/FDS04/project (4th_school) $ cat css/test.css
html {
  font-size: 10px; }

body {
  font-size: 1.4rem;
  color: #333; }

a {
  color: #333; }
gose:~/FDS04/project (4th_school) $ clear

gose:~/FDS04/project (4th_school) $ node-sass sass/test.scss -o css/ --output-style compact
Rendering Complete, saving .css file...
Wrote CSS to /Users/gose/FDS04/project/css/test.css
gose:~/FDS04/project (4th_school) $ cat css/test.css
html { font-size: 10px; }

body { font-size: 1.4rem; color: #333; }

a { color: #333; }
gose:~/FDS04/project (4th_school) $ node-sass sass/test.scss -o css/ --output-style expaneded
Rendering Complete, saving .css file...
Wrote CSS to /Users/gose/FDS04/project/css/test.css
gose:~/FDS04/project (4th_school) $ cat css/test.css
html {
  font-size: 10px; }

body {
  font-size: 1.4rem;
  color: #333; }

a {
  color: #333; }
gose:~/FDS04/project (4th_school) $ node-sass sass/test.scss -o css/ --output-style compressed
Rendering Complete, saving .css file...
Wrote CSS to /Users/gose/FDS04/project/css/test.css
gose:~/FDS04/project (4th_school) $ cat css/test.css
html{font-size:10px}body{font-size:1.4rem;color:#333}a{color:#333}
gose:~/FDS04/project (4th_school) $ node-sass sass/test.scss -o css/ --output-style nested
Rendering Complete, saving .css file...
Wrote CSS to /Users/gose/FDS04/project/css/test.css
gose:~/FDS04/project (4th_school) $ cat css/test.css
html {
  font-size: 10px; }

body {
  font-size: 1.4rem;
  color: #333; }

a {
  color: #333; }
gose:~/FDS04/project (4th_school) $ node-sass sass/test.scss -o css/ --output-style expanded
Rendering Complete, saving .css file...
Wrote CSS to /Users/gose/FDS04/project/css/test.css
gose:~/FDS04/project (4th_school) $ cat css/test.css
html {
  font-size: 10px;
}

body {
  font-size: 1.4rem;
  color: #333;
}

a {
  color: #333;
}
gose:~/FDS04/project (4th_school) $ node-sass -w sass/ -o css/ --output-style expanded
=> changed: /Users/gose/FDS04/project/sass/test.scss
Rendering Complete, saving .css file...
Wrote CSS to /Users/gose/FDS04/project/css/test.css
=> changed: /Users/gose/FDS04/project/sass/test.scss
Rendering Complete, saving .css file...
Wrote CSS to /Users/gose/FDS04/project/css/test.css
=> changed: /Users/gose/FDS04/project/sass/test.scss
Rendering Complete, saving .css file...
Wrote CSS to /Users/gose/FDS04/project/css/test.css
=> changed: /Users/gose/FDS04/project/sass/test.scss
Rendering Complete, saving .css file...
Wrote CSS to /Users/gose/FDS04/project/css/test.css
^C
gose:~/FDS04/project (4th_school) $ 