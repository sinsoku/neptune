# 漁師が作る料理サイト

## 現在の問題点

* 漁師が捕まえても需要がなくて売れない魚（以下雑魚）がある
* 雑魚は漁師の方が自分で食べたり、捨てられている
* 雑魚でも美味しい魚も多い
* 雑魚の料理法を消費者が知らない

## 目的

* 廃棄される雑魚の数を減らしたい
* もったいない

## 概要

漁師の方が日常的に作っている料理を投稿できるサイト。
また、美味しそうなレシピから魚を注文し、配送してもらえる。

## 仕様

### 料理

* 漁師、消費者はログインできる
* 漁師は料理を投稿できる
* 漁師は料理に使った魚を登録できる
* 消費者は料理に使われた魚を知ることができる
* ユーザは料理に画像を添付できる

### EC

* ユーザは料理に使われている魚を注文できる
* ユーザは注文された魚を発送できる
* ユーザは販売可能な魚を登録できる
* 発送者は発送ステータスを変更できる

### 時間的に無理そう

* ユーザは料理に動画を添付できる

## 懸念点

* 漁師の方の手間が多いと、料理が投稿されない
* 漁港によって直売はタブーになっているケースがある

## DB設計

```
users
- name
- role
- address
- fishing_port_name

cookbooks
- user_id
- title
- description

cookbook_fishes
- cookbook_id
- fish_id

orderable_fishes
- user_id
- fish_id

fishes
- name

media
- cookbook_id
- url

order
- user_id
- dest_user_id
- status

order_boxes
- order_id
- delivery_number
```

## URL設計

```
root 'cookbooks#index'
# cookbooks
resources :users
resources :cookbooks
resources :media, only: [:create, :destroy]
resources :fishes
# EC
resources :order
resources :order_boxes
```
