# Flutter Chess Application

Flutterで開発されたチェスアプリ。作り方は非常に簡単で、Flutter入門には非常におすすめである。20~30分で簡単に作れるのでオススメ。(**というかコピペで動く**)

# 開発手順

## インストール

まずは以下のコマンドを叩く

```powershell
\> flutter create <project-name> # ちなみに本プロジェクトではchessapp
\> cd <project-name>
\> flutter pub get flutter_chess_board
```

## `pubspec.yaml`への記入

| :exclamation:        | TFlutterパッケージをインストールした後この作業は必要不可欠である。**以下の作業を忘れるとアプリが正常に動作しないので要注意。パッケージをインストールした後は必ずこれをやること。**       |
|---------------|:------------------------|

```yaml
dependencies:
  flutter:
    sdk: flutter

  cupertino_icons: ^1.0.2
  flutter_chess_board: ^1.0.1 #ここはよく忘れるので要注意！
```

## サンプル

とりあえず以下のプログラムを`lib/main.dart`へコピペしよう。

```dart
import 'package:flutter/material.dart';
import 'package:flutter_chess_board/flutter_chess_board.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: const HomePage(),
    );
  }
}

class HomePage extends StatefulWidget {
  const HomePage({Key? key}) : super(key: key);

  @override
  _HomePageState createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  ChessBoardController controller = ChessBoardController();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Chess Demo'),
      ),
      body: Column(
        children: [
          Expanded(
            child: Center(
              child: ChessBoard(
                controller: controller,
                // 盤面の色
                boardColor: BoardColor.orange,
                // 盤面に矢印が表示される
                arrows: [
                  BoardArrow(
                    from: 'd2',
                    to: 'd4',
                    //color: Colors.red.withOpacity(0.5),
                  ),
                  BoardArrow(
                    from: 'e7',
                    to: 'e5',
                    color: Colors.red.withOpacity(0.7),
                  ),
                ],
                // プレイヤーの色をここで表示する
                boardOrientation: PlayerColor.white,
              ),
            ),
          ),
          Expanded(
            child: ValueListenableBuilder<Chess>(
              valueListenable: controller,
              builder: (context, game, _) {
                return Text(
                  controller.getSan().fold(
                        '',
                        (previousValue, element) =>
                            '${previousValue} \n' + (element ?? ''),
                      ),
                );
              },
            ),
          ),
        ],
      ),
    );
  }
}
```

完成画面は以下の通り。

# 開発環境

* Windows 11
* Visual Studio Code 1.67
* flutter_chess_board 1.0.1 - dart package
* dart 2.17.0
* Google Chrome