# 読解ノート：自分のアプリのコード3箇所

> **氏名：** （自分の名前）
> **AI利用レベル：** 1（質問のみ。説明は自分の言葉で書く）
> **最終更新：** YYYY-MM-DD

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
（この部分が果たしている役割を説明する）

**なぜこう書くのか：**
（別の書き方ではなく、この書き方が選ばれている理由を説明する。分からなければ「分からない」と書いてよい）

**もしこう書かなかったら：**
（この部分を消したり変えたりすると何が起きるか。実際に試した結果があればここに書く）

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

**なぜこう書くのか：**

**もしこう書かなかったら：**

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

**なぜこう書くのか：**

**もしこう書かなかったら：**

---

## 自分ではまだ説明できない箇所（正直に）

（アプリの中で「動いているけれど何をしているか分からない」ところを書く。ここに書いたものは、後期の文法の授業で分かるようになります。）
