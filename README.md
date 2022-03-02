
# downnload mongo e descompactar
curl https://fastdl.mongodb.org/osx/mongodb-macos-x86_64-5.0.6.tgz

# Mac
https://docs.mongodb.org/manual/tutorial/install-mongodb-on-os-x/

# Linux (ubuntu)
https://docs.mongodb.org/manual/tutorial/install-mongodb-on-ubuntu/

# Windows
https://docs.mongodb.org/manual/tutorial/install-mongodb-on-windows/


# no bashrc
alias "start_mongodb= ~/mongodb/bin/mongod --dbpath ~/mongodb/db/"
alias "mongo= ~/mongodb/bin/mongo"
alias "mongorestore= /Users/danilo/mongodb/bin/mongorestore"
alias "mongodump= /Users/danilo/mongodb/bin/mongodump"

//https://www.mongodb.com/pt-br/basics/create-database
show dbs

//Para criar um banco de dados você usa o comando use. Se o banco de dados não existir, então o cluster do MongoDB irá criá-lo.
use myshinynewdb


# criar coleção

db.createCollection("alunos")

# insert
db.alunos.insert({
    "nome" : "Danilo", 
    "email": "danilo@teste.com",
    "data_nascimento" : new Date (1983,12,09)
})


db.alunos.insert({
    "nome": "Felipe",
    "data_nascimento": new Date(1994, 02, 26),
    "curso": {
        "nome": "Sistemas de informação"
    },
    "notas": [10.0, 9.0, 4.5],
    "habilidades": [{
        "nome": "inglês",
        "nível": "avançado"
    }, {
        "nome": "taekwondo",
        "nível": "básico"
    }]
})


db.alunos.insert(
{"nome" : "Julio",
"data_nascimento" : new Date(1972, 08, 30),
"curso" : {
    "nome" : "Medicina"
},
"habilidades" : [
        {
        "nome" : "inglês",
        "nível" : "avançado"
        }    
    ]
}
)


# busca
db.alunos.find()

# remover
db.alunos.remove({
    "_id" : ObjectId ("56cb0002b6d75ec12f75d3b5")
})


# busca

db.alunos.find(
    {
        nome : "Danilo"
    }
)

db.alunos.find(
    {
        nome : "Danilo"
    }
).pretty()

# Buscando com dado relacional
db.alunos.find({ "habilidades.nome" : "inglês" }).pretty()


# busca com and
db.alunos.find({
    "curso.nome" : "Sistemas de informação",
    "curso.nome" : "Engenharia Química"
    })

# buscar com or
db.alunos.find({
    $or : [
        {"curso.nome" : "Sistemas de informação"},
        {"curso.nome" : "Engenharia Química"}    
    ]
})

# busca com or e and
db.alunos.find({
    $or : [
        {"curso.nome" : "Sistemas de informação"},
        {"curso.nome" : "Engenharia Química"}    
    ],
    "nome" : "Daniela"
})

 db.alunos.find({
     $or : [
        {"curso.nome" : "Sistemas de informação"},
        {"curso.nome" : "Engenharia Química"},
        {"curso.nome" : "Moda"}
    ],
    "nome" : "Daniela"
 })

 # busca com in

 db.alunos.find({
    "curso.nome" : {
        $in : ["Sistema de informação", "Engenharia Química"]
        }
})
