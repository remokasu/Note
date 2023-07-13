 # python -m <package_name>
`__main__.py`ファイルをプロジェクトのルートディレクトリに作成し、その中でメイン関数を呼び出す

~~~python
from package_name import main

if __name__ == "__main__":
    main()
~~~

* インストールすると、次のコマンドで呼び出し可能
~~~bash
python -m <package_name>
~~~

<br>

# パッケージ化
### 1 プロジェクトの構造を作成する
~~~
your_project/
├── your_project/
│   ├── __init__.py
│   ├── subpackage1/
│   │   ├── __init__.py
│   │   ├── module1.py
│   │   ├── module2.py
│   │   └── ...
│   ├── subpackage2/
│   │   ├── __init__.py
│   │   ├── module1.py
│   │   ├── module2.py
│   │   └── ...
│   └── ...
├── tests/
├── setup.py
├── README.md
└── LICENSE
~~~

setup.py内のfind_packages()関数が各サブパッケージを自動的に見つける。<br>
各サブディレクトリが独自の__init__.pyファイルを持つことで、それぞれがPythonパッケージとして認識される。<br>
パッケージのインポートは次のように記述<br>

~~~
from your_project.subpackage1 import module1
from your_project.subpackage2 import module2
~~~

### 2. setup.py を作成
~~~ python
from setuptools import setup, find_packages

setup(
    name="your_project",
    version="0.0.1",
    url="https://github.com/yourname/your_project",
    author="Author Name",
    author_email="author@gmail.com",
    description="Description of your project",
    packages=find_packages(),  # 自動的にパッケージとサブパッケージを見つける
    install_requires=["numpy", "pandas"],  # 依存関係をリストで提供
    classifiers=[
        'Programming Language :: Python :: 3.9',
    ]
)
~~~
