# Lab9.3

from flask import Flask, render_template_string, request
 
app = Flask(__name__)
 
# สถานะของหลอด LED
led_status = {
    'led1': 'OFF',
    'led2': 'OFF'
}
 
@app.route('/', methods=['GET', 'POST'])
def index():
    if request.method == 'POST':
        led = request.form.get('led')
        state = request.form.get('state')
        if state == 'on':
            led_status[led] = 'ON'
        elif state == 'off':
            led_status[led] = 'OFF'
   
    return render_status()
 
def render_status():
    return render_template_string('''
        <h1>LED Status</h1>
        <p>LED 1 - {{ status_led1 }}</p>
        <p>LED 2 - {{ status_led2 }}</p>
        <h2>Control LEDs</h2>
        <form method="POST">
            <h3>LED 1</h3>
            <button name="led" value="led1" type="submit" name="state" value="on">Turn ON</button>
            <button name="led" value="led1" type="submit" name="state" value="off">Turn OFF</button>
 
            <h3>LED 2</h3>
            <button name="led" value="led2" type="submit" name="state" value="on">Turn ON</button>
            <button name="led" value="led2" type="submit" name="state" value="off">Turn OFF</button>
        </form>
    ''', status_led1=led_status['led1'], status_led2=led_status['led2'])
 
if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0')
