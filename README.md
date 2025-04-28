from flask import Flask, request, redirect, render_template_string, url_for
import uuid

app = Flask(__name__)
letters = {}  # This will temporarily store letters in memory

# HTML templates
write_template = '''
<!doctype html>
<html>
<head>
    <title>Write Your Love Letter 💌</title>
</head>
<body style="font-family: Arial; background: linear-gradient(to right, #ffdde1, #ee9ca7); text-align:center; padding-top:50px;">
    <h1>Write Your Love Letter 💌</h1>
    <form method="post">
        <textarea name="letter" rows="10" cols="40" placeholder="Write your love here..." style="border-radius:10px; padding:10px;"></textarea><br><br>
        <button type="submit" style="background-color:#ff6f91; padding:10px 20px; border:none; border-radius:10px; color:white;">Create Link</button>
    </form>
</body>
</html>
'''

link_template = '''
<!doctype html>
<html>
<head>
    <title>Your Love Letter Link</title>
</head>
<body style="font-family: Arial; background: #ffe4e1; text-align:center; padding-top:50px;">
    <h1>Your Link is Ready! ✨</h1>
    <p>Share this link:</p>
    <a href="{{ url }}">{{ url }}</a>
</body>
</html>
'''

read_template = '''
<!doctype html>
<html>
<head>
    <title>Love Letter 💖</title>
</head>
<body style="font-family: Arial; background: linear-gradient(to right, #ffdde1, #ee9ca7); text-align:center; padding-top:50px;">
    <h1>Someone Sent You a Love Letter 💖</h1>
    <div style="background:white; margin:auto; padding:20px; width:50%; border-radius:10px; box-shadow: 0 0 10px pink;">
        <p style="white-space: pre-wrap;">{{ letter }}</p>
    </div>
</body>
</html>
'''

@app.route('/', methods=['GET', 'POST'])
def write_letter():
    if request.method == 'POST':
        letter = request.form['letter']
        letter_id = str(uuid.uuid4())
        letters[letter_id] = letter
        return render_template_string(link_template, url=request.host_url + 'letter/' + letter_id)
    return render_template_string(write_template)

@app.route('/letter/<letter_id>')
def read_letter(letter_id):
    letter = letters.get(letter_id)
    if letter:
        return render_template_string(read_template, letter=letter)
    else:
        return "<h1>Letter not found 💔</h1>", 404

if __name__ == '__main__':
    app.run(debug=True)
