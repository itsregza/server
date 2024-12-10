const express = require('express');
const fs = require('fs');
const path = require('path');

const app = express();
app.use(express.json());

const KEYS_FILE = path.join(__dirname, 'license-keys.txt');

app.post('/verify', (req, res) => {
    const { licenseKey } = req.body;
    
    fs.readFile(KEYS_FILE, 'utf8', (err, data) => {
        if (err) {
            return res.status(500).json({ valid: false, error: 'Server error' });
        }
        
        const validKeys = data.split('\n').map(key => key.trim()).filter(Boolean);
        const isValid = validKeys.includes(licenseKey);
        
        res.json({ valid: isValid });
    });
});

app.listen(3000, () => {
    console.log('License server running on port 3000');
});
