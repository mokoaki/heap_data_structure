# heap(データ構造)

```text
              0
      1               2
  3       4       5       6
7   8   9  10   11 12   13 14
```

- いわゆる「ヒープ領域」は別物
- 他にも改良型のヒープが存在する

## とりあえず基本的なバイナリヒープぽい動きをするオブジェクトを実装して遊ぶ

```sh
gem update --system
gem update bundler
# bundle install --path=.bundle/gems --jobs=4 --clean
bundle install
bundle exec rspec
```

```ruby
require './src/heap_object'

heap = Heap.new
heap.push(3)
heap.push(2).push(5)
heap.push(4, 6, 1)

heap.pop
# => 1
heap.pop(3)
# => [2, 3, 4]
heap.pop_all
# => [5, 6]
```

## バイナリヒープソートを実装して遊ぶ

- バイナリヒープソートは安定ソートではない
- もっとも、Array#sort自体が安定ソートではない

```ruby
require './src/array_heap_sort'

items = [3, 2, 5, 4, 6, 1]

items.heap_sort
# => [1, 2, 3, 4, 5, 6]
items
# => [3, 2, 5, 4, 6, 1]

items.heap_sort!
# => [1, 2, 3, 4, 5, 6]
items
# => [1, 2, 3, 4, 5, 6]
```

## 実装してみてわかったこと

- ヒープの唯一の存在理由↓についてはヒープが早い、何十倍も早い( ･`ω･´)
  - 「優先順位が一番高い要素の参照はO(1)、popはO(log n)」
- ソート目的でArray#heap_sortを実装してもArray#sortの方が早い、何十倍も早い(´・ω・`)
  - ビルトインクラス先輩パねぇっす(´・ω・`)
