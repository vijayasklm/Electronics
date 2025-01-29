# Electronics--
const mongoose = require('mongoose');
const Product = require('../models/Product'); // Import the Product model

// Connect to MongoDB
mongoose.connect('mongodb://127.0.0.1:27017/productsDB', {
    useNewUrlParser: true,
    useUnifiedTopology: true
}).then(() => console.log("MongoDB connected"))
  .catch(err => console.log("MongoDB connection error:", err));

// Query to find Electronics with price > 500, sorted by price descending
async function findExpensiveElectronics() {
    try {
        const products = await Product.find({
            category: "Electronics",
            price: { $gt: 500 }
        }).sort({ price: -1 });

        console.log("Expensive Electronics Products:", products);
    } catch (error) {
        console.error("Error fetching products:", error);
    } finally {
        mongoose.connection.close(); // Close connection after query execution
    }
}

// Execute the query
findExpensiveElectronics();

npm install mongoose

node queries/findExpensiveElectronics.js
Expensive Electronics Products: [
    {
        "_id": "65a1234bcde5678f90123456",
        "title": "Gaming Laptop",
        "price": 1500,
        "category": "Electronics",
        "inStock": true
    },
    {
        "_id": "65a1234bcde5678f90123457",
        "title": "4K Smart TV",
        "price": 900,
        "category": "Electronics",
        "inStock": true
    }
]


