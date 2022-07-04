require('dotenv').config();
const jwt = require('jsonwebtoken');
const router = require('express').Router();
const { phone } = require('../controllers');

function AuthenticateAccessToken(req,res,next){
    const authHeader = req.headers['authorization'];
    const token = authHeader && authHeader.split(' ')[2];
    console.log(process.env.ACCESS_TOKEN_SECRET);
    console.log(token);
    
    if(token == null){
        res.json({ message: 'Invalid access token'});
    }
    else{
        jwt.verify(token, process.env.ACCESS_TOKEN_SECRET, (err,user) => {
            if(err){
                res.json({ message: err });
            }
            else{
                
                next();
            }
        });
    }
}

// GET localhost:8080/phone => Ambil data semua phone
router.get('/phone', AuthenticateAccessToken, phone.getDataPhone);

// GET localhost:8080/phone/2 => Ambil data semua phone berdasarkan id = 2
router.get('/phone/:id', phone.getDataPhoneByID);

// POST localhost:8080/phone/add => Tambah data phone ke database
router.post('/phone/add', phone.addDataPhone);

// POST localhost:8080/phone/2 => Edit data phone
router.post('/phone/edit', phone.editDataPhonr);

// POST localhost:8080/phone/delete => Delete data phone
router.post('/phone/delete/', phone.deleteDataPhone);

module.exports = router;