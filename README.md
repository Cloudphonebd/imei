<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cloud Phone IMEI Submission</title>
    <style>
        body { 
            font-family: 'Arial', sans-serif; 
            background-color: #f4f7f9; 
            display: flex; 
            justify-content: center; 
            align-items: center; 
            height: 100vh; 
            margin: 0; 
        }
        .container { 
            background: #ffffff; 
            padding: 30px; 
            border-radius: 15px; 
            box-shadow: 0 8px 30px rgba(0,0,0,0.1); 
            width: 90%; 
            max-width: 400px; 
            text-align: center; 
        }
        h2 { 
            font-size: 20px; 
            color: #333; 
            margin-bottom: 20px; 
            line-height: 1.5;
        }
        input[type="text"] { 
            width: 100%; 
            padding: 12px; 
            margin-bottom: 20px;
            border: 2px solid #ddd; 
            border-radius: 8px; 
            font-size: 16px; 
            box-sizing: border-box;
        }
        input[type="text"]:focus {
            border-color: #007bff;
            outline: none;
        }
        button { 
            background-color: #007bff; 
            color: white; 
            border: none; 
            padding: 15px; 
            width: 100%; 
            border-radius: 8px; 
            font-size: 18px; 
            font-weight: bold; 
            cursor: pointer; 
            transition: 0.3s;
        }
        button:hover { 
            background-color: #0056b3; 
        }
        .footer {
            margin-top: 25px;
            font-size: 14px;
            color: #888;
        }
    </style>
</head>
<body>

<div class="container">
    <h2>Submit your IMEI number here to get all the apps of Cloud Phone.</h2>
    
    <form action="https://formspree.io/f/xeezzqnp" method="POST">
        <input type="text" name="IMEI_Number" placeholder="Enter 15-digit IMEI" required minlength="15" maxlength="15">
        <button type="submit">Submit</button>
    </form>

    <div class="footer">
        © Cloud phone BD
    </div>
</div>

</body>
</html>
