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