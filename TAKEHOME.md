# TAKE HOME TEST

1. Get the source code of tree.

```bash
pull-lp-source tree jammy
mv tree-2.0.2 tree-ppa
cd tree-ppa/
git init
git add .
git commit -m "initial commit tree (2.0.2-1)"
```

2. add a bash script "testing.sh"

```bash
quilt new take-home.patch
quilt add testing.sh
quilt add Makefile
quilt header -e
vi testing.sh
```

3. modify "Makefile" to copy "testing.sh" to /usr/bin

```bash
vi Makefile
quilt refresh
```

4. add a maintainer script "debian/postinst"

```bash
cp testing.sh debian/postinst
```

5. build and dput PPA

```bash
dch -i
debuild -S
git add .
git commit -m "take-home.patch"
cd ..
cat ~/.dput.cf
# [pseudoc]
# fqdn = ppa.launchpad.net
# method = ftp
# incoming = ~pseudoc/ubuntu/ppa/
# login = anonymous
# allow_unsigned_uploads = 0
dput pseudoc tree_2.0.2-yuze1_source.changes
```

6. another patch to fix the missing slash in shebang.

```bash
quilt new shebang.patch
quilt add testing.sh
vi testing.sh
cp testing.sh debian/posinst
quilt refresh
quilt header -e
```

7. build and dput PPA again

```bash
dch -i
debuild -S
git add .
git commit -m "shebang.patch"
cd ..
dput pseudoc tree_2.0.2-yuze2_source.changes
```
