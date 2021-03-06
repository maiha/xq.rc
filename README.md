# xq.cr

Command-line XML processor inspired by `jq`

## Installation

#### Static Binary is ready for x86_64 linux
- https://github.com/maiha/xq.cr/releases

## Usage

```shell
% cat aho.xml
<ul><li>foo</li><li>bar</li></ul>
```

#### v0.1.0
- formatting with `.`

```shell
% cat aho.xml | xq .
<?xml version="1.0"?>
<ul>
  <li>foo</li>
  <li>bar</li>
</ul>
```

#### v0.2.0
- css filtering that starts with "."

```shell
% cat aho.xml | xq .li
<li>foo</li>
<li>bar</li>
```

#### v0.3.0
- css filtering with case-ignore

```shell
% cat aho.xml | xq -i .LI
<li>foo</li>
<li>bar</li>
```

## Development

- Assumed that we are using `ubuntu-16.04` and `crystal-0.22.x`.

Please install `libxml2.a` first as bellow.

```shell
make
```

### static libxml2.a

We can't link statically against libxml2 due to lack of `ICU_XXX` in `ubuntu-16.04`.
So we manually build `libxml2.a` without icu first.

```
apt-get install automake # for `aclocal`
apt-get install liblzma-dev
apt-get install python2.7-dev
apt-get source libxml2
cd libxml2-2.9.3+dfsg1
./configure --with-python=no --with-trio=no --with-http=no --with-ftp=no
make

sudo mv /usr/lib/x86_64-linux-gnu/libxml2.a{,.dist}
sudo cp -p .libs/libxml2.a /usr/lib/x86_64-linux-gnu/
```

## Contributing

1. Fork it ( https://github.com/maiha/xq.cr/fork )
2. Create your feature branch (git checkout -b my-new-feature)
3. Commit your changes (git commit -am 'Add some feature')
4. Push to the branch (git push origin my-new-feature)
5. Create a new Pull Request

## Contributors

- [maiha](https://github.com/maiha) maiha - creator, maintainer
