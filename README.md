Vize ödevi
Commit işlemleri yaptıktan sonra main yazmak istediğimde hata aldım bu yüzden işlemler master kısmında yer aldı. 
git push -u origin master yaptım daha sonra güncelleme ile main kısmına alamadım. 
İlk ödevde de bu repoyu paylaştığım için yeni bir repo açamadım.
Commit işlemleri master kısmında yer almaktadır.

26.12.2024 Final Ödevi
vize ödevinde java kodu kullanmıştım. final ödevinde python kodunu yazdım. projeyi vs code üzerinden yaptım ancak python kodunda get ve post işlemlerini yazan kodu yazdığım zaman systemctl start uygulama07 -> systemctl status uygulama07 dediğim zaman kütüphane kurulumundan beri hata veriyor. ben de sadece toplama ve çarpma işlemleri yapan kodu yazarak ilerledim. ödevin içerieğinde olan GNU/Linux sistemler için systemctl ile yönetilebilecek servis oluşturulması gibi işlemleri yaptım. 
python kodunda yazdığım get ve post işlemleri kullandığım kod ektedir.
from flask import Flask, request, jsonify
from flasgger import Swagger

app = Flask(_name_)
swagger = Swagger(app)

@app.route('/add', methods=['GET', 'POST'])
def add():
    """
    Add two numbers
    ---
    parameters:
      - name: num1
        in: query
        type: number
        required: true
        description: First number
      - name: num2
        in: query
        type: number
        required: true
        description: Second number
    responses:
      200:
        description: Result of addition
        schema:
          type: object
          properties:
            result:
              type: number
    """
    if request.method == 'POST':
        data = request.json
        num1 = data.get('num1')
        num2 = data.get('num2')
    else:
        num1 = request.args.get('num1', type=float)
        num2 = request.args.get('num2', type=float)

    if num1 is None or num2 is None:
        return jsonify({'error': 'Both num1 and num2 are required'}), 400
    
    result = num1 + num2
    return jsonify({'result': result})

@app.route('/multiply', methods=['GET', 'POST'])
def multiply():
    """
    Multiply two numbers
    ---
    parameters:
      - name: num1
        in: query
        type: number
        required: true
        description: First number
      - name: num2
        in: query
        type: number
        required: true
        description: Second number
    responses:
      200:
        description: Result of multiplication
        schema:
          type: object
          properties:
            result:
              type: number
    """
    if request.method == 'POST':
        data = request.json
        num1 = data.get('num1')
        num2 = data.get('num2')
    else:
        num1 = request.args.get('num1', type=float)
        num2 = request.args.get('num2', type=float)

    if num1 is None or num2 is None:
        return jsonify({'error': 'Both num1 and num2 are required'}), 400
    
    result = num1 * num2
    return jsonify({'result': result})

if _name_ == '_main_':
    app.run(debug=True)

    bu kod çalıştığı zaman toplama işlemi için= http://127.0.0.1:5000/add?num1=5&num2=3
    çarpma işlemi için= http://127.0.0.1:5000/multiply?num1=5&num2=3
