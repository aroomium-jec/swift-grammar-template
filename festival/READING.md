# 読解ノート：自分のアプリのコード3箇所

> **氏名：** 吉田香
> **AI利用レベル：** 1（質問のみ。説明は自分の言葉で書く）
> **最終更新：** 2026-10-19

生成AIに書いてもらったコードでも、自分で書いたコードでもかまいません。自分のアプリの中から3箇所を選んで、次の3つの問いに答えてください。分からないところは、生成AIに「この行は何をしていますか」「この行を消すとどうなりますか」と聞いてかまいません。ただし、書くのは自分の言葉です。

> 💡 担任の先生の指示で、項目が増えることがあります。

---

## 箇所1：デッキ編成の画面を開くボタン <!-- [HomeView.swift の93〜99行目 (line 93)](/Users/cmstudent/Documents/授業26CM/1年後期/Swift/日専祭/ByonByonMen/ios/HackYou/HackYou/HomeView.swift:93)  -->
```swift 
// 該当部分のコードを抜粋して貼る（5〜15行くらい）
NavigationLink {
    DeckManagerView()
} label: {
    pairButton(title: "デッキ編成", subtitle: "", icon: "rectangle.stack.fill")
}
.buttonStyle(HomeTileStyle(aqua: aqua))
.homeButtonSound()
```

**何をしているか：**
- 「デッキ編成」という文字とカードのアイコンを表示する。
- 押すと、`DeckManagerView`というデッキ管理画面へ移動する。
- ボタンの見た目を整え、押したときに効果音を鳴らす。

**なぜこう書くのか：**
- NavigationLinkを使うと、`NavigationStack`の中で次の画面へ移動でき、戻る操作も利用できる。

**もしこう書かなかったら：**
- NavigationLinkによる画面遷移がなければ、このボタンからデッキ編成画面を開けない。
- .buttonStyle(...)を外すと、独自の背景・枠線・押したときの色の変化がなくなる。
- .homeButtonSound()を外すと、このボタンの操作音が鳴らなくなる。

---

## 箇所2：音量を調整するスライダー <!-- [SettingsView.swift の38〜52行目 (line 38)](/Users/cmstudent/Documents/授業26CM/1年後期/Swift/日専祭/ByonByonMen/ios/HackYou/HackYou/SettingsView.swift:38) -->

```swift
// コードを貼る
private struct VolumeRow: View {
    @Binding var value: Float

    var body: some View {
        HStack(spacing: 10) {
            Image(systemName: "speaker.fill")
                .foregroundStyle(.secondary)
                .frame(width: 20)
            Slider(value: $value, in: 0...1)
            Image(systemName: "speaker.wave.3.fill")
                .foregroundStyle(.secondary)
                .frame(width: 24)
        }
        .padding(.vertical, 2)
    }
```

**何をしているか：**
- 小さいスピーカー、スライダー、大きいスピーカーを横に並べる。
- スライダーで音量を`0〜1`の範囲で変更する。
- BGMと効果音の両方で、同じ`VolumeRow`を使っている。

**なぜこう書くのか：**
- @Bindingを使い、設定画面から渡された音量の値とつなげている。
- $valueは、スライダーが値を読み取るだけでなく、変更もできるように渡す書き方。

**もしこう書かなかったら：**
- 親の音量とつながない別の値を変更しても、実際の音量設定には反映されない。
- このコードで`$value`を単に`value`に変えると、スライダーが必要とする値の渡し方と合わず、コンパイルエラーになる。

---

## 箇所3：新しいデッキを作って保存する処理<!-- [DeckStore.swift の138〜144行目 (line 138)](/Users/cmstudent/Documents/授業26CM/1年後期/Swift/日専祭/ByonByonMen/ios/HackYou/HackYou/DeckStore.swift:138) -->

```swift
// コードを貼る
@discardableResult
func createDeck(name: String, faction: Faction) -> String {
    let d = SavedDeck(name: name.isEmpty ? "新しいデッキ" : name, faction: faction)
    decks.append(d)
    save()
    return d.id
}
```

**何をしているか：**
- 名前と陣営を受け取って、新しい空のデッキを作る。
- 名前が空なら「新しいデッキ」という名前にする。
- デッキ一覧に追加して端末へ保存し、作成したデッキのIDを返す。

**なぜこう書くのか：**
- name.isEmpty ? "新しいデッキ" : nameで、名前が入力されているかによって使う名前を選べる。
- appendは、配列の末尾に新しいデッキを追加する処理。
- save()で、一覧のデータを端末に保存する。
- IDを返すと、呼び出した側で作成したデッキを特定できる。
- @discardableResultは、返されたIDを使わない場合も警告が出ないようにする指定。

**もしこう書かなかったら：**
- 空の名前への対応を外すと、名前が空のデッキが作られる。
- decks.append(d)を消すと、作ったデッキが一覧に追加されない。
- save()を消すと、この処理の時点では端末に保存されず、再起動後に残らない可能性がある。
- Stringを残したまま`return d.id`を消すと、戻り値がないためコンパイルエラーになる。

---

## 自分ではまだ説明できない箇所（正直に）

（アプリの中で「動いているけれど何をしているか分からない」ところを書く。ここに書いたものは、後期の文法の授業で分かるようになります。）
