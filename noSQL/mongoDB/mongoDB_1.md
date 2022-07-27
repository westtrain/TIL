# MongoDB 설치 및 실행과 CRUD 사용법
- 터미널에서 설치 및 실행
    
    ```jsx
    brew install mongodb
    vi ~/.zshrc
    // 아래의 코드를 추가
    export MONGO_PATH=/usr/local/mongodb/bin
    export PATH=$PATH:$MONGO_PATH
    // 다시 CLI로 돌아와서 dbpath 설정
    cd ~
    sudo mkdir -p data/db
    sudo chown <username> ./data/db
    // MongoDB 서버 실행
    mongodb --dbpath=/Users/{username}/data/db
    // 이제 서버 작동, 새로운 터미널 열고 몽고디비 실행
    mongo
    ```
    
- Database 생성 : use
    
    ```jsx
    use mongodb_tutorial // mongodb_tutorial db 생성
    db                   // 현재 사용중인 DB 확인
    show dbs             // 데이터베이스 리스트 확인
    // 방금 만든 mongodb_tutorial이 없는 이유 = 최소 한개의 Document가 추가되야 함
    db.book.insert({"name": "MongoDB Tutorial", "author": "Josh"});
    show dbs             // 이제 데이터베이스 리스트에서 mongodb_tutorial 확인 가능
    ```
    
- Database 제거 : db.dropDatabase()
    
    ```jsx
    use mongodb_tutorial // mongodb_tutorial로 변경
    db.dropDatabase();   // 데이터베이스 삭제
    show dbs             // mongodb_tutorial 데이터베이스가 삭제되어 나타나지 않음
    ```
    
- Collection 생성 : db.createCollection([컬렉션 이름],[options])
    
    ```jsx
    // Collection 생성에는 options을 넣을 수 있음(선택 사항)
    db.createCollection(name, [options])
    // name = 생성하려는 컬렉션 이름. 
    db.createCollection("author"); // author라는 이름의 컬랙션 생성
    db.createCollection("author", capped: true, authIndex: true, size: 6142800, max: 10000});
    // createCollection을 사용하지 않고 document에 추가하면 자동 생성도 됨
    db.[collectionName].insert({"name":{documentUserName}});
    db.age.insert({"name":"Josh"}) // Josh 이름 가지고 있는 document에 age 컬렉션 추가 생성
    show collections               // collection list 확인
    ```
    
    - Option list
        
        
        | Field | Type | Desc |
        | --- | --- | --- |
        | capped | Boolean | 이 값을 true로 설정하면 capped collection을 활성화 시킴. Capped Collection이란, 고정된 크기(fixed size)를 가진 컬렉션으로서, size가 초과되면 가장 오래된 데이터를 덮어씁니다. 이 값을 true로 설정하면 size값을 꼭 설정해야 한다. |
        | autoIndex | Boolean | 이 값을 true로 설정하면, _id 필드에 index를 자동으로 생성함. 기본값은 false |
        | size | number | Capped collection을 위해 해당 컬렉션의 최대 사이즈를 ~bytes로 지정함 |
        | max | number | 해당 컬렉션에 추가 할 수 있는 최대 갯수를 설정함 |
- Collection 제거 : db.[collection name].drop()
    
    ```jsx
    use mongodb_tutorial // mongodb_tutorial로 변경
    show collections     // Collection list 확인
    db.age.drop()        // age collection 삭제
    ```
    
- Document 추가 : db.[collection name].insert(document)
    
    ```jsx
    // 한개의 document에 books컬렉션을 추가하는 경우
    db.books.insert({"name": "mongodb_toturial", "author": "Josh"});
    // 두개의 document에 books컬렉션을 추가하는 경우, 배열을 이용함
    db.books.insert([
    					{"name": "mongodb_toturial1", "author": "Josh"},
    					{"name": "mongodb_toturial2", "author": "Josh"}
    ]);
    // books컬렉션의 document list 확인
    db.books.find();
    ```
    
- Document 제거 : db.[collection name].remove(crieria, justOne)
    
     
    
    ```jsx
    // books컬렉션에서 'name'이 'mongodb_tutorial1'인 다큐먼트 제거
    db.books.find({"name": "mongodb_tutorial1"});
    db.books.remove({"name": "mongodb_tutorial1"});
    db.books.find() // mongodb_tutorial1이 삭제됨 확인
    ```
    
    Parameters
    
    | parameters | type | description |
    | --- | --- | --- |
    | criteria | document | 삭제할 데이터의 기준 값(criteria). 값이 {}이면 컬렉션의 모든 데이터 제거 |
    | justOne | boolean | 선택적(Optional) 매개변수로 값이 true면 1개의 다큐멘트만 제거. 생략되면 기본값은 false이면, criteria에 해당하는 모든 다큐멘트 제거 |
