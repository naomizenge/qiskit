Qiskit のインストールとセットアップ
===================================


前提ソフトウエア
----------------

Qiskit を使用するには
`Python 3.5 以上 <https://www.python.org/downloads/>`__ が必要です。
また対話的に `tutorials`_ を行う場合、
`Jupyter Notebooks <https://jupyter.readthedocs.io/en/latest/install.html>`__ を使用すると効率的です。

個別にインストールするか、`Anaconda 3 <https://www.anaconda.com/download/>`__ python ディストリビューションを
インストールしてください。Anaconda 3 にはこれらすべての前提ソフトウエアが含まれています。

Windows ユーザーは追加で VC++ ランタイムコンポーネントのインストールも必要です。以下のリンクのどちらかを使用してインストールしてください。

- `Microsoft Visual C++ Redistributable for Visual Studio 2017 <https://go.microsoft.com/fwlink/?LinkId=746572>`__
- `Microsoft Visual C++ Redistributable for Visual Studio 2015 <https://www.microsoft.com/en-US/download/details.aspx?id=48145>`__


環境と Qiskit のインストール
-----------------------------

.. note::

    `Python 仮想環境 <https://docs.python.org/3/tutorial/venv.html>`__ の利用を推奨します。
    他のアプリケーションから Qiskit 環境を分離し不要なトラブルを避けられます。


もっとも簡単に環境を使用するには Anaconda を使用してください。

.. code:: sh

     conda create -y -n Qiskitenv python=3
     activate Qiskitenv


Qiskit のインストールには PIP ツール (Python パッケージマネージャー) を使用してください。

.. code:: sh

    pip install qiskit

最新の安定版リリースと、依存パッケージがインストールされます。

ビジュアライゼーション用のパッケージを含めたインストール
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Qiskit に含まれるすべてのビジュアライゼーション機能を使用するには、追加のパッケージが必要です。
次のコマンドを実行すると Qiskit と同時に、すべてのビジュアライゼーション機能に必要なパッケージをインストールします。

.. code:: sh

   pip install qiskit[visualization]



スタンドアロン版のセットアップ
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Qiskit の拡張を目的としてインストールする場合は個別にリポジトリをクローンし、各リポジトリのインストール手順に従ってください。

- `Terra リポジトリ <https://github.com/Qiskit/qiskit-terra>`__
- `Aer リポジトリ <https://github.com/Qiskit/qiskit-aer>`__
- `Aqua リポジトリ <https://github.com/Qiskit/qiskit-aqua>`__
- `Chemistry リポジトリ <https://github.com/Qiskit/qiskit-chemistry>`__


API トークンと IBMQ 認証情報の構成
---------------------------------------------

-  まだ持っていなければ `IBM Q <https://quantumexperience.ng.bluemix.net>`__ アカウントを作成してください。
-  IBM Q Web サイトにログインし、“My Account” > “Advanced” から API トークンを取得してください。


認証情報の自動ロード
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

IBM Q 量子装置のアクセス認証情報は自動的にロードされるため、IBM Q 認証の設定は非常に簡単です。
インストール後に一度だけ API 認証情報を設定するか保存すれば、
あとは使用する際に次のコードを実行するだけで済みます。

.. code:: python

    from qiskit import IBMQ

    IBMQ.load_accounts()

この ``IBMQ.load_accounts()`` 呼び出しは、(必要であれば) 複数の場所から自動的に認証情報のロードを実行し、
IBM Q に対して認証し、プログラム用にオンライン装置を利用可能にします。
次のどちらかの方法を使用して、認証情報を保存してください。


API 認証情報のローカルへの保存
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

大部分のユーザーにとって一番簡単な方法は API 認証情報の保存でしょう。
情報はローカルの構成ファイル「`qiskitrc`」に保存され、一度保存すると、あとは
プログラム内で明示的に渡さずに認証情報を使用できます。

情報を保存するには、次のコマンドを実行してください。

.. code:: python

    from qiskit import IBMQ

    IBMQ.save_account('MY_API_TOKEN')


このとき `MY_API_TOKEN` はトークンで置き換えてください。

「IBM Q ネットワーク」上にいる場合には、`IBMQ.save_account()` に 
q-console アカウントページに表示される `url` 引数を渡す必要があります。
さらに追加の情報 (例: プロキシー情報) が必要な場合もあります。

.. code:: python

    from qiskit import IBMQ

    IBMQ.save_account('MY_API_TOKEN', url='https://...')



認証情報の手動ロード
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

より複雑なシナリオの場合や複数アカウントに対するきめ細かい制御が必要な場合は、
API トークン、および他のパラメータを直接 ``IBMQ.enable_account()`` 関数に渡すことができます。
このとき、認証情報は自動でロードされず、引数の値が直接、使用されます。

.. code:: python

    from qiskit import IBMQ

    IBMQ.enable_account('MY_API_TOKEN', url='https://my.url')



この例では ``MY_API_TOKEN`` と指定した URL を使用して認証されます。構成ファイルに保存された構成や、
環境変数、``Qconfig.py`` は無視されます。

``Qconfig.py`` から手動でロードするには、次のコマンドを実行してください。

.. code:: python

    from qiskit import IBMQ
    import Qconfig

    IBMQ.enable_account(Qconfig.APIToken, **Qconfig.config)


複数の認証情報を使用する方法の詳細については ``qiskit.IBMQ`` ドキュメントを参照してください。


トラブルシューティング
-------------------------

このドキュメントで紹介したインストール手順は、セットアップにおける Python 環境の知識
を前提としています(例: 標準の Python、``virtualenv``、Anaconda)。
それぞれのドキュメントで環境に応じた手順を参照してください。

システムや設定によっては、``pip install`` コマンドの前に「sudo -H」を付ける必要があります。

.. code:: sh

    pip install -U --no-cache-dir qiskit



.. _tutorials: https://github.com/Qiskit/qiskit-tutorial
