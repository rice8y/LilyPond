# LilyPond

- [LilyPond](#lilypond)
- [LilyPondとは](#lilypondとは)
- [LilyPondの導入](#lilypondの導入)
- [LilyPondの使い方](#lilypondの使い方)
- [LilyPondによる楽譜作成例](#lilypondによる楽譜作成例)
  - [Hanon No.1](#hanon-no1)

## LilyPondとは

LilyPondとは, GPLライセンスのもとにフリーで公開されているクロスプラットフォームの楽譜作成ソフトウェアである. LilyPondはC++で記述され, Schemeライブラリでアセンブルされているが, ユーザ独自のカスタマイズや拡張も可能である.

## LilyPondの導入

ここでは, LilyPondの導入手順について述べる. ただし, エディタの導入が済んでいることを前提とする. また, 本記事ではエディタとしてVScodeを使用し, OSはWindowsであることを前提として述べる.

1. [LilyPondの公式ウェブサイト](https://lilypond.org/doc/v2.23/Documentation/web/download)から最新バージョンのソフトウェアをダウンロードする.
2. ダウンロードしたインスラーを実行してLilyPondをインストールする.

上記の手順でLilyPondをインストール出来たら動作確認を行う.
`cmd`で`lilypond --v`として以下のような出力が得られれば良い. 

```cmd
GNU LilyPond 2.24.3 (running Guile 2.2)

Copyright (c) 1996--2023 by
  Han-Wen Nienhuys <hanwen@xs4all.nl>
  Jan Nieuwenhuizen <janneke@gnu.org>
  and others.

This program is free software.  It is covered by the GNU General Public
License and you are welcome to change it and/or distribute copies of it
under certain conditions.  Invoke as `lilypond --warranty' for more
information.
```

LilyPondが正常に動作しない場合は, ローカル環境にパスを通すことで改善されるかもしれない.

## LilyPondの使い方

大まかな使い方としては以下の通りである.

1. エディタで楽譜をテキストで記述する (拡張子は".ly").
2. 以下の要領でコンパイルする.

```cmd
lilypond sample.ly
```

3. PDFとMDMIが出力される.

以降では, LilyPindにおける楽譜の記述方法について述べる.

## LilyPondによる楽譜作成例

### Hanon No.1

hanon01.ly：

```cmd
\version "2.24.3"
\language "english"

\paper {
    top-margin = 2.0\cm
    bottom-margin = 2.0\cm
    line-width = 17\cm
    indent = 0\cm
}

\header
{
  title = "Hanon No.1"
  composer = "Charles-Louis Hanon"
}

upper = \relative c'' {
  \time 2/4
  \clef trable
  \tempo 4 = 108
  \numericTimeSignature
  s1 | s1 | g,16 [ b c d ] e16 [ d c b ] |
  \break
  \stemUp
  a16 [ c d e ] f16 [ e d c ] | b16 [ d e f ] g16 [ f e d ] | c16 [ e f g ] a16 [ g f e ] | d16 [ f g a ] b16 [ a g f ] | e16 [ g a b ] c16 [ b a g ] |
  \break
  \stemUp
  f16 [ a b c ] 
  \stemDown
  d16 [ c b a ] | 
  g16 [ b c d ] e16 [ d c b ] | a16 [ c d e ] f16 [ e d c ] | b16 [ d e f ] g16 [ f e d ] \bar "||" g16^\markup{\tiny 5} [ e^\markup{\tiny 4} d^\markup{\tiny 3} c^\markup{\tiny 2} ] b16^\markup{\tiny 1} [ c^\markup{\tiny 2} d^\markup{\tiny 3} e^\markup{\tiny 4} ] |
  \break
  \stemDown
  f16^\markup{\tiny 5} [ d c b ] a16 [ b c d ] | e16 [ c b a ] 
  \stemUp
  g16 [ a b c ] | d16 [ b a g ] f16 [ g a b ] | c16 [ a g f ] e16 [ f g a ] | b16 [ g f e ] d16 [ e f g ] |
  \break
  \stemUp
  a16 [ f e d ] c16 [ d e f ] | g16 [ e d c ] b16 [ c d e ] | f16 [ d c b ] a16 [ b c d ] | e16 [ c b a ] g16 [ a b c ] | s1 | s1 | s1 |
}

lower = \relative c {
  \time 2/4
  \clef bass
  << \new Voice {
    \stemUp
    c16^\markup{\tiny 1} [ e^\markup{\tiny 2} f^\markup{\tiny 3} g^\markup{\tiny 4} ] a16^\markup{\tiny 5} [ g^\markup{\tiny 4} f^\markup{\tiny 3} e^\markup{\tiny 2} ] }
    \new Voice {
      \stemDown
      c,16_\markup{\tiny 5} [ e_\markup{\tiny 4} f_\markup{\tiny 3} g_\markup{\tiny 2} ] a16_\markup{\tiny 1} [ g f e] }
  >> |
  << \new Voice {
    \stemUp
    d'16^\markup{\tiny 1} [ f g a ] b16 [ a g f ] }
    \new Voice {
      \stemDown
      d,16_\markup{\tiny 5} [ f g a ] b16 [ a g f ] } 
  >> |
  << \new Voice {
    \stemUp
    e'16 [ g a b ] c16 [ b a g ] } 
    \new Voice {
      \stemDown
      e,16 [ g a b ] c16 [ b a g ] }
  >> | 
  << \new Voice {
    \stemUp
    f'16 [ a b c ] d16 [ c b a ] }
    \new Voice {
      \stemDown
      f,16 [ a b c ] d16 [ c b a ] }
  >> | 
  g16 [ b c d ] e16 [ d c b ] |
  \break
  \stemUp
  a16 [ c d e ] 
  \stemDown
  f16 [ e d c ] |
  b16 [ d e f ] g16 [ f e d ] | c16 [ e f g ] a16 [ g f e ] | d16 [ f g a ] b16 [ a g f ] | e16 [ g a b ] c16 [ b a g ] |
  \break
  \stemDown
  f16 [ a b c ] d16 [ c b a ] | g16 [ b c d ] e16 [ d c b ] | a16 [ c d e ] f16 [ e d c ] | b16 [ d e f ] g16 [ f e d ] \bar "||" g16_\markup{\tiny 1} [ e_\markup{\tiny 2} d_\markup{\tiny 3} c_\markup{\tiny 2} ] b16_\markup{\tiny 1} [ c_\markup{\tiny 2} d_\markup{\tiny 3} e_\markup{\tiny 4} ] |
  \break
  \stemDown
  f16_\markup{\tiny 1} [ d c b ] a16 [ b c d ] | e16 [ c b a ] g16 [ a b c ] | d16 [ b a g ] f16 [ g a b ] | c16 [ a g f ] e16 [ f g a ] | b16 [ g f e ] d16 [ e f g ] |
  \break
  \stemDown
  a16 [ f e d ] c16 [ d e f ] | g16 [ e d c ] 
  \stemUp
  b16 [ c d e ] | f16 [ d c b ] a16 [ b c d ] | e16 [ c b a ] g16 [ a b c ] |
  << \new Voice {
    \stemUp
    d'16 [ b a g ] f16 [ g a b ] }
    \new Voice {
      \stemDown 
      d,16 [ b a g ] f16 [ g a b ] }
  >> |
  \break
  << \new Voice {
    \stemUp
    c'16 [ a g f ] e16 [ f g a ] }
    \new Voice {
      \stemDown 
      c,16 [ a g f ] e16 [ f g a ] }
  >> |
  << \new Voice {
    \stemUp
    b'16 [ g f e ] d16 [ e f g ] }
    \new Voice {
      \stemDown 
      b,16 [ g f e ] d16 [ e f g ] }
  >> |
  << \new Voice {
    \stemUp
    a'16 [ f e d ] c16 [ d e f ] }
    \new Voice {
      \stemDown 
      a,16 [ f e d ] c16 [ d e f ] }
  >> |
  << \new Voice {
    \stemUp
    g'16 [ e d c ] b16 [ c d e ] }
    \new Voice {
      \stemDown 
      g,16 [ e d c ] b16 [ c d e ] }
  >> |
  \bar ":|." 
  << \new Voice {
    \stemUp
    c'2 }
    \new Voice {
      \stemDown
      c,2 } 
  >> \bar "|."
}

\score {
  \context PianoStaff <<
    \new Staff {
      \upper
    }
    \new Staff {
      \lower
    }
  >>
  \layout {
    \override Score.Clef.break-visibility = #all-invisible
    \override Score.KeySignature.break-visibility = #all-invisible
    \override Score.SystemStartBar.collapse-height = #1
  }
  \midi {}
}
```

hanon01.pdf：

![hanon01](hanon01.png)
