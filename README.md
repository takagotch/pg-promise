### pg-promise
---
https://github.com/vitaly-t/pg-promise

```js
db.any('SELECT * FROM product WHERE price BETWEEN $1 AND $2', [1, 10])
db.any('SELECT * FROM users WHERE name = $1', 'John')

db.any('SELECT * FROM users WHERE name = ${name} AND active = $/active/', {
  name: 'John',
  active: true
})

db.none('INSERT INTO documents(id, doc) VALUES(${id}, ${this})', {
  id: 123,
  body: 'some text'
})

db.query('SELECT $1:name FROM $2:name', ['*', 'table']);

db.query('SELECT ${columns:name} FROM ${table:name}', {
  columns: ['column1', 'column2'],
  table: 'table'
});

const obj = {
  one: 1,
  two: 2
};
db.query('SELECT $1:name FROM $2:name', [obj, 'table']);

const obj = {
  one: 1,
  two: 2
};
db.query('INSERT INTO table($(this:name)) VALUES(${this:csv})', obj);

db.any('SELECT full_name as $1:alias FROM $2:name', ['name', 'table']);

const where = pgp.as.format('WHERE price BETWEEN $1 AND $2', [5, 10]);
db.any('SELECT * FROM products $1:raw', where);

const name = 'John';
const filter = '%' + name + '%';

const obj = {
  toPostgres(self) {
  }
}

const obj = {
  toPostgres(self) {
  },
  rawType: true
}

class STPoint {
  constructor(x, y) {
    this.x = x;
    this.y = y;
    this.rawTypw = true;
  }
  
  toPostgres(self) {
    return pgp.as.format('ST_MakePoint($1, $2)', [this.x, this.y]);
  }
}

function STPoint(x, y) {
  this.rawType = true;
  this.toPostgres = () => pgp.as.format('ST_MakePoint($1, $2)', [x, y]);
}

Date.prototype.toPostgres = a => a.getTime();

const ctf = pgp.as.ctf;

const obj = {
  [ctf.toPostgres](self){
    // self = this = obj
  },
  [ctf.rawType]: true
};

const ctf = {
  toPostgres: Symbol.for('ctf.toPostgres'),
  rawType: Symbol.for('ctf.rawType')
};

db.task(t => {
  return t.one('SELECT count(*) FROM events WHERE id = $1', 123, a => +a.count)
    .then(count => {
      if(count > 0) {
        return t.any('SELECT * FROM log WHERE event_id = $1', 123)
          .then(logs => {
            return {count, logs};
          })
      }
      return {count};
    });
})
  .then(data => {
    // success, data = either {count} or {count, logs}
  })
  .catch(error => {
    // failed
  })

db.tx(t => {
  const q1 = t.none('UPDATE users SET active = $1 WHERE id = $2', [true, 123]);
  const q2 = t.one('INSERT INTO audit(entity, id) VALUES($1, $2) RETURNING id', ['users', 123]);
  
  return t.batch([q1, q2]);
})
  .then(data => {
  })
  .catch(error => {
  })
  
const TransactionMode = pgp.txMode.TransactionMode;
const isolationLevel = pgp.txMode.isolationLevel;

const mode = new TransactionMode({
  tiLevel: isolationLevel.seralizable,
  readOnly: true,
  deferrable: true
});

db.tx({mode}, t => {
})
  .then(() => {
  })
  .catch(error => {
  });
  
db.$pool.end();

.finally(db.$pool.end);

pgp.end();

.finally(pgp.end);
```

```sql
SELECT * FROM table WHERE name LIKE '%$1:value%')
```

```
BEGIN ISOLATION LEVEL SERIALIZABLE READ ONLY DEFERABLE
```


