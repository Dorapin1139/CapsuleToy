# 重なる券（1.2）

今までのコード付き券に加えて、同じ券を複数枚重ねて持てます。名前は「infernalカプセルトイ券」です。色は薄紫の太字、説明は灰色の 3 行です。

1. 看板の 1 行目を `[capsuletoy]`、2 行目を `infernal` にして設置します。2 行目は英数字と `_` だけです。
2. `/capsuletoy modify infernal` のあと、景品を入れたチェストを右クリックします。
3. チェストの中身が景品です。空の枠はハズレです。同じ品を複数の枠に置くと、その品が出やすくなります。中身は `/im getloot <番号>` で出した実物を入れてください。
4. `stack-ticket-names` に書いた名前の看板だけが、この重なる券を受け付けます。コード付きの券は、今までどおり別の看板で使えます。
5. 券を手に持って看板を右クリックすると、1 枚減ります。チェストから枠を 1 つランダムにもらえます。空の枠なら、券は減ったまま何も出ません。持ち物に入りきらない景品は、その束が足元に落ちます。

設定が既にあるサーバでは、`config.yml` に次が無いとき、プラグインは同じ既定値を使います。

```yaml
stack-ticket-display-name: "&d&linfernalカプセルトイ券"
stack-ticket-lore1: "&7infernalカプセルトイで使えます。"
stack-ticket-lore2: "&7ランダムなinfernalmobsのアイテムと交換できます。"
stack-ticket-lore3: "&7一部出ないアイテムもあります。"
stack-ticket-names:
  - infernal
dropped-pick: "インベントリが一杯なので、足元に落としました。"
```

渡すコマンドは `/capsuletoy stackticket <プレイヤー> [枚数]` です。枚数は 1 から 64 です。

# Migration from ver1.0 to ver1.1
~~~
# cd plugins/CapslueToy/
# cp -p sqlite.db sqlite.db.backup
# sqlite3 ./sqlite.db
sqlite> DROP INDEX world_name_sign_xyz_uindex;
sqlite> DROP INDEX world_name_chest_xyz_uindex;
sqlite> .output ./old_ticket_code.txt
sqlite> select 'INSERT INTO ticket (ticket_code) values (''' || ticket_code || ''');' from ticket;
sqlite> .quit
# cp ./old_ticket_code.txt ../CapsuleToy/
# cp -p ./sqlite.db ../CapsuleToy/
cd ./CapsuleToy
sqlite3 ./sqlite.db < ./old_ticket_code.txt
~~~

# Fixed a spelling mistake.
Works with capsuletoy instead of capsluetoy. The sign needs to be redone.
