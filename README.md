# examen-mongodb
//crear base de datos 
use anime_store
mongo import --db.anime_store -- colections products-- file data_anime_store
db.products.countdocuments()
db.products.findone()

//agregar producto 
db.products.insertone({
    
        "sku": "A101",
        "name": "Figura Naruto Uzumaki",
        "category": "Figuras",
        "price": 120000,
        "stock": 10,
        "anime": "Naruto",
        "rating": 4.8,
        "tags": ["coleccionable", "resina", "edición especial"],
        "provider": {
        "name": "OtakuDistribuciones",
        "country": "Japón"
        }
        
})
//Agregar a todos los productos las siguientes propiedades:
db.products.updatemany(
    {}
    {$set:
        {available: true,
​        origin: "Importado"
    }
    })
db.products.findone()

//Realizar las siguientes actualizaciones:

//​ Producto con sku: A034, actualizar stock a 15.
db.products.updateone(
    {"sku":A034},
    {$set:{"stock":15}}
)

//Producto con sku: A018, cambiar el country del provider a "Colombia".
db.products.updateone(
    {"sku":A018},
    {$set:{"place.country":"colombia"}}
)

//Producto con sku: A059, agregar un nuevo tag: "oferta".
db.products.updateone(
    {"sku":A059},
    {$push:{"tag":"oferta"}}
)

 //Producto con sku: A012, agregar dos nuevos tags: "nuevo", "popular".
 db.products.updateone(
    {"sku":A012},
    {$push:{"tag":{$each:["nuevo","popular"]}}}
)

//Producto con sku: A025, agregar los tags "descuento", "outlet".
db.products.updateone(
    {"sku":A025},
    {$push:{"tag":{$each:["descuento","outlet"]}}}
)

//Producto llamado "Camiseta Goku Ultra Instinct", cambiar el price a 45000.
db.updtaeone(
    {"name":"Camiseta Goku Ultra Instinct"},
    {$set:{"price":45000}}
)

//Renombrar la propiedad origin a import_type.
db.products.updatemany(
    {},
    {$rename:{"origin":"import_type"}})
db.products.findone({},{"origin":1,"import_type":1})

//Cambiar el import_type a "Nacional" para los productos cuyo proveedor esté en Colombia.
db.products.updatemany(
    {"place.country":"colombia"},
    {$set:{"import_type":"nacional"}}
)

//Mostrar los productos de la categoría "Mangas"
db.products.find({"category":"mangas"})

//Mostrar los productos que tienen un precio mayor a 50000
db.products.countdocuments({"price":{$gte:50000}})

//Mostrar los productos que no son de la categoría "Figuras"
db.products.countdocuments({"category":{$not:"Figuras"}})

//Mostrar el sku, name y tags de los productos que tienen calificación mayor a 4.5.
db.products.find(
    {rating:{$gte:4.5}},
    {"sku":0,"name":1,"tags":1})

    //Mostrar sku, name, y price de los productos con stock menor a 5.
    db.products.find(
        {stock:{$lt:5}},
        {"sku":0,"name":1,"price":1})

//Eliminar la propiedad available de todos los documentos.
db.products.updatemany(
    {$pull:{propety:{$in:{"available"}}}}
)

//Eliminar el tag "descuento" del producto con sku: A025.

db.products.UpdateOne(
    {sku:A025},
    {$pull:{"tag":"descuento"}}
)
