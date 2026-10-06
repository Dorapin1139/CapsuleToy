# コード付きの券（1.2）

スロットの景品は、コード付きの券です。当たった枚数だけ、1 枚ずつ別の番号で渡します。どのカプセルトイの看板でも使えます。使った番号は消え、同じ紙を複製しても、そのあとは使えません。重なる券は使いません。

1. 看板の 1 行目を `[capsuletoy]`、2 行目を `infernal` にして設置します。2 行目は英数字と `_` だけです。
2. `/capsuletoy modify infernal` のあと、景品を入れたチェストを右クリックします。
3. チェストの中身が景品です。同じ品を複数の枠に置くと、その品が出やすくなります。中身は `/im getloot <番号>` で出した実物を入れてください。
4. コード付きの券を手に持って看板を右クリックすると、1 枚減ります。チェストから枠を 1 つランダムにもらえます。持ち物に入りきらない景品は、足元に落ちます。

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
