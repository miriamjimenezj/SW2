1. En la colección sales indique cuántos clientes con edades comprendidas entre 50 y 70 incluidas (age dentro de customer) han comprado algo haciendo uso de un cupón (couponUsed a true)
   db.sales.find({
    "customer.age": { $gte: 50, $lte: 70 },
    "couponUsed": true
}).count();

3. En la colección sales muestre para cada venta unicamente el total de esa venta (la suma de todos los price dentro de items), la fecha de la venta (saleDate) y el correo del cliente (email dentro de customer). Ordene los resultados por total de venta de mayor a menor.

db.sales.aggregate([
    {
        $project: {
            total: { $sum: "$items.price" },
            saleDate: 1,
            email: "$customer.email"
        }
    },
    {
        $sort: { total: -1 }
    }
]);

   
5. En la colección sales indique el número de ventas que contienen al menos un backpack y un notepad (name dentro de items)

db.sales.find({
    "items.name": { $all: ["backpack", "notepad"] }
}).count();

   
7. En la colección sales indique cuántas ventas están asociadas a cada valor de satisfacción (satisfaction dentro de customer)

   db.sales.aggregate([
    {
        $group: {
            _id: "$customer.satisfaction",
            count: { $sum: 1 }
        }
    }
]);

