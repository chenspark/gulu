echo "# gulu" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/chenspark/gulu.git
git push -u origin master

git remote add origin https://github.com/chenspark/gulu.git
git push -u origin master
/*****加了参数-u后，以后即可直接用git push 代替git push origin master*********/

BDD  behavior dirven development  行为驱动开发=》用自然语言描述需求should expect assert,三种方式

TDD  test dirven development      测试驱动开发

Assert     断言
console.assert()只能判断真和假