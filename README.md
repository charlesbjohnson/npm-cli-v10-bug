# npm-cli-v10-bug

## Environment

```sh
$ node -v
v22.1.0

$ npm -v
10.7.0
```

## Steps to Reproduce

```sh
$ git clone https://github.com/charlesbjohnson/npm-cli-v10-bug.git
$ cd npm-cli-v10-bug/

$ npm install

$ npm --verbose update follow-redirects

npm verbose cli /home/ec2-user/.asdf/installs/nodejs/22.1.0/bin/node /home/ec2-user/.asdf/installs/nodejs/22.1.0/bin/npm
npm info using npm@10.7.0
npm info using node@v22.1.0
npm verbose title npm update follow-redirects
npm verbose argv "--loglevel" "verbose" "update" "follow-redirects"
npm verbose logfile logs-max:10 dir:/home/ec2-user/.npm/_logs/2024-05-09T04_26_05_476Z-
npm verbose logfile /home/ec2-user/.npm/_logs/2024-05-09T04_26_05_476Z-debug-0.log
npm http fetch GET 200 https://registry.npmjs.org/follow-redirects 96ms (cache hit)

... hangs ...
```

## Additional Context

<details>
<summary>Debug Logs</summary>

```
1 info using npm@10.7.0
2 info using node@v22.1.0
3 silly config:load:file:/home/ec2-user/.asdf/installs/nodejs/22.1.0/lib/node_modules/npm/npmrc
4 silly config:load:file:/home/ec2-user/npm-cli-v10-bug/.npmrc
5 silly config:load:file:/home/ec2-user/.npmrc
6 silly config:load:file:/home/ec2-user/.asdf/installs/nodejs/22.1.0/etc/npmrc
7 verbose title npm update follow-redirects
8 verbose argv "--loglevel" "verbose" "update" "follow-redirects"
9 verbose logfile logs-max:10 dir:/home/ec2-user/.npm/_logs/2024-05-09T04_26_05_476Z-
10 verbose logfile /home/ec2-user/.npm/_logs/2024-05-09T04_26_05_476Z-debug-0.log
11 silly logfile done cleaning log files
12 silly idealTree buildDeps
13 silly fetch manifest follow-redirects@^1.15.0
14 http fetch GET 200 https://registry.npmjs.org/follow-redirects 96ms (cache hit)
15 silly placeDep ROOT follow-redirects@1.15.6 REPLACE for: axios@1.6.0 want: ^1.15.0
```

</details>

---

<details>
<summary>Works in <a href="https://github.com/npm/cli/releases/tag/v10.3.0"><code>npm@10.3.0</code></a></summary>

```sh
$ npx -y npm@10.3.0 --verbose update follow-redirects
npm verb cli /home/ec2-user/.asdf/installs/nodejs/22.1.0/bin/node /home/ec2-user/.npm/_npx/b66e65489868d75c/node_modules/.bin/npm
npm info using npm@10.3.0
npm info using node@v22.1.0
npm verb title npm update follow-redirects
npm verb argv "--loglevel" "verbose" "update" "follow-redirects"
npm verb logfile logs-max:10 dir:/home/ec2-user/.npm/_logs/2024-05-09T04_27_10_228Z-
npm verb logfile /home/ec2-user/.npm/_logs/2024-05-09T04_27_10_228Z-debug-0.log
npm http fetch GET 200 https://registry.npmjs.org/follow-redirects 128ms (cache hit)
npm http fetch GET 200 https://registry.npmjs.org/follow-redirects/-/follow-redirects-1.15.6.tgz 85ms (cache miss)
npm info run @contrast/fn-inspect@3.3.1 install node_modules/@contrast/fn-inspect node-gyp-build
npm http fetch POST 200 https://registry.npmjs.org/-/npm/v1/security/advisories/bulk 204ms
npm info run @contrast/fn-inspect@3.3.1 install { code: 1, signal: null }
npm verb reify failed optional dependency /home/ec2-user/npm-cli-v10-bug/node_modules/@contrast/fn-inspect
npm verb reify failed optional dependency /home/ec2-user/npm-cli-v10-bug/node_modules/node-gyp-build

changed 1 package, and audited 241 packages in 2s

7 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
npm verb exit 0
npm info ok
```

</details>

---

<details>
<summary>Broken as of <a href="https://github.com/npm/cli/releases/tag/v10.4.0"><code>npm@10.4.0</code></a></summary>

```sh
$ npx -y npm@10.4.0 --verbose update follow-redirects
npm verb cli /home/ec2-user/.asdf/installs/nodejs/22.1.0/bin/node /home/ec2-user/.npm/_npx/8daac0b3d3a63617/node_modules/.bin/npm
npm info using npm@10.4.0
npm info using node@v22.1.0
npm verb title npm update follow-redirects
npm verb argv "--loglevel" "verbose" "update" "follow-redirects"
npm verb logfile logs-max:10 dir:/home/ec2-user/.npm/_logs/2024-05-09T04_27_52_807Z-
npm verb logfile /home/ec2-user/.npm/_logs/2024-05-09T04_27_52_807Z-debug-0.log
npm http fetch GET 200 https://registry.npmjs.org/follow-redirects 124ms (cache hit)

... hangs ...
```

</details>
