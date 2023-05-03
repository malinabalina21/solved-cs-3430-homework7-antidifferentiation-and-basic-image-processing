Download Link: https://assignmentchef.com/product/solved-cs-3430-homework7-antidifferentiation-and-basic-image-processing
<br>
Antidifferentiation

Splitting, Merging, and Amplifying Images

<h1>Warmup</h1>

Practice antidifferentiation on the problems below. For those of you who are familiar with integration, the term <strong>antidifferentiation </strong>is synonymous with <strong>indefinite integration </strong>and <strong>definite antidifferentiation </strong>– with <strong>definite integration</strong>. I use the term <strong>antidifferentiation</strong>, because it is common in scientific computing and numerical analysis, but the terms are completely interchangeable. If and when you feel comfortable with antidifferentiation, move on to Problem 1. We’ll turn these problems into your unit tests for Problem 1.

<ol>

 <li><sup>R </sup><em>x</em><sup>2</sup><em>dx</em>; <strong>answer: </strong>is real;</li>

 <li><sup>R </sup><em>e</em><sup>−2<em>x</em></sup><em>dx</em>; <strong>answer: </strong>is real;</li>

</ol>

√

<ol start="3">

 <li><sup>R </sup><em>xdx</em>; <strong>answer:</strong>is real;</li>

 <li>; <strong>answer: </strong> is real;</li>

 <li>; <strong>answer: </strong><em>ln</em>|<em>x</em>| + <em>C</em>, <em>C </em>is real;</li>

 <li>; <strong>answer: </strong> is real;</li>

 <li><sup>R </sup>4<em>x</em><sup>3</sup><em>dx</em>; <strong>answer: </strong><em>x</em><sup>4 </sup>+ <em>C</em>, <em>C </em>is real;</li>

 <li><sup>R </sup>(5<em>x </em>− 7)<sup>−2</sup><em>dx</em>; <strong>answer: </strong>is real.</li>

 <li>; <strong>answer: </strong>3<em>ln</em>|2 + <em>x</em>| + <em>C</em>, <em>C </em>is real.</li>

</ol>

<h1>10.           <sup>R </sup>(3<em>x </em>+ 2)<sup>4 </sup><em>dx</em>; answer: is real. Problem 1: Antidifferentiation</h1>

Implement the function antideriv(i) in the file antideriv.py that takes an integrand <em>i </em>represented as a function expression and outputs an antiderivative of <em>i </em>also represented as a function expression. Let’s make a simplifying assumption that the value of <em>C </em>in the returned antiderivative is always 0.

Your implementation should handle the following four main cases: 1) <em>i </em>is a constant; 2) <em>i </em>is a power; 3) <em>i </em>is a sum; 4) <em>i </em>is a product in which the first element is a constant. In case 2, let <em>b </em>be the base of <em>i </em>and <em>d </em>be its degree. Then, case 2, in turn, splits into the following three subcases: 2.1) <em>b </em>is a variable and <em>d </em>is a constant; 2.2) <em>b </em>= <em>e</em>; 2.3) <em>b </em>is a sum. I gave you the code outline in antideriv.py where you should implement and save your code.

<h2>Test 01</h2>

Let’s do <sup>R </sup><em>x</em><sup>2</sup><em>dx</em>.

from maker import make_e_expr, make_prod, make_const from maker import make_plus, make_pwr, make_ln from maker import make_pwr_expr, make_quot from antideriv import antideriv from tof import tof

def test_01():

print(’
***** Test 01 ***********’) fex = make_pwr(’x’, 2.0) print(fex) afex = antideriv(fex) assert not afex is None def gt(x): return (1.0/3.0)*(x**3.0) afexf = tof(afex) assert not afexf is None err = 0.0001 for i in range(1, 101):

assert abs(afexf(i) – gt(i)) &lt;= err

print(afex) print(’Test 01: pass’) Here is the output of test_01 in the Py shell. ***** Test 01 *********** (x^2.0)

(((1.0/3.0)*(x^3.0))+0.0) Test 01: pass

<h2>Test 02</h2>

Let’s do <sup>R </sup><em>e</em><sup>−2<em>x</em></sup><em>dx</em>.

def test_02():

print(’
***** Test 02 ***********’) fex = make_e_expr(make_prod(make_const(-2.0), make_pwr(’x’, 1.0)))

print(fex) afex = antideriv(fex) assert not afex is None def gt(x): return (-0.5)*(math.e**(-2.0*x)) afexf = tof(afex) assert not afexf is None err = 0.0001 for i in range(0, 101):

assert abs(afexf(i) – gt(i)) &lt;= err

print(afex) print(’Test 02: pass’)

Here is the output of test_02 in the Py shell.

***** Test 02 ***********

(2.71828182846^(-2.0*(x^1.0)))

(((1.0/-2.0)*(2.71828182846^(-2.0*(x^1.0))))+0.0) Test 02: pass

<h2>Test 03</h2>

√

Let’s do <sup>R </sup><em>x</em>.

def test_03():

print(’
***** Test 03 ***********’) fex = make_pwr(’x’, 0.5) print(fex) afex = antideriv(fex) assert not afex is None def gt(x): return (2.0/3.0)*(x**(3.0/2.0)) afexf = tof(afex) assert not afexf is None

err = 0.0001 for i in range(1, 101):

assert abs(afexf(i) – gt(i)) &lt;= err

print(afex) print(’Test 03: pass’)

Here is the output of test_03 in the Py shell.

***** Test 03 *********** (x^0.5)

(((1.0/1.5)*(x^1.5))+0.0)

Test 03: pass

<h2>Test 04</h2>

Let’s do.

def test_04():

print(’
***** Test 04 ***********’) fex = make_pwr(’x’, -2.0) print(fex) afex = antideriv(fex) assert not afex is None def gt(x): return -1.0/x afexf = tof(afex) assert not afexf is None err = 0.0001 for i in range(1, 101):

assert abs(afexf(i) – gt(i)) &lt;= err

print(afex) print(’Test 04: pass’)

Here is the output of test_04 in the Py shell.

***** Test 04 ***********

(x^-2.0)

(((1.0/-1.0)*(x^-1.0))+0.0)

Test 04: pass

<h2>Test 05</h2>

Let’s do.

def test_05():

print(’
***** Test 05 ***********’) fex = make_pwr(’x’, -1.0) print(fex) afex = antideriv(fex) assert not afex is None afexf = tof(afex) assert not afexf is None def gt(x): return math.log(abs(x), math.e) err = 0.0001 for i in range(1, 101): assert abs(afexf(i) – gt(i)) &lt;= err

for i in range(-100, 0):

assert abs(afexf(i) – gt(i))

print(’Test 05: pass’)

Here is the output of test_05 in the Py shell.

***** Test 05 ***********

(x^-1.0)

(ln|(x^1.0)|+0.0)

Test 05: pass

<h2>Test 06</h2>

Let’s do . I did not use numerical comparison assertions in this unit test, because the values become huge pretty fast. Instead, I just printed the first ten outputs of the ground truth function and the antiderivative function.

def test_06():

print(’
***** Test 06 ***********’) fex1 = make_pwr(’x’, -3.0) fex2 = make_prod(make_const(7.0), make_e_expr(make_prod(make_const(5.0), make_pwr(’x’, 1.0))))

fex3 = make_prod(make_const(4.0), make_pwr(’x’, -1.0))

fex4 = make_plus(fex1, fex2) fex = make_plus(fex4, fex3) print(fex) afex = antideriv(fex) assert not afex is None print(afex) def gt(x):

v1 = -0.5*(x**(-2.0)) v2 = (7.0/5.0)*(math.e**(5.0*x)) v3 = 4.0*(math.log(abs(x), math.e)) return v1 + v2 + v3

afexf = tof(afex) assert not afexf is None err = 0.0001 for i in range(1, 10): print(afexf(i), gt(i))

#assert abs(afexf(i) – gt(i)) &lt;= err print(’Test 06: pass’)

Here is the output of test_06 in the Py shell.

***** Test 06 ***********

(((x^-3.0)+(7.0*(2.71828182846^(5.0*(x^1.0)))))+(4.0*(x^-1.0)))

(((((((1.0/-2.0)*(x^-2.0))+0.0)+((7.0*(((1.0/5.0)*

(2.71828182846^(5.0*(x^1.0))))+0.0))+0.0))+0.0)


((4.0*(ln|(x^1.0)|+0.0))+0.0))+0.0)

(207.2784227436072, 207.2784227436072)

(30839.699701451627, 30839.699701451624)

(4576628.66035455, 4576628.66035455)

(679231279.0876331, 679231279.087633)

(100806859078.75783, 100806859078.75781)

(14961064414141.379, 14961064414141.377)

(2220418833238806.8, 2220418833238806.5)

(3.295393735718273e+17, 3.2953937357182726e+17)

(4.890797948047902e+19, 4.8907979480479015e+19)

Test 06: pass

<h2>Test 07</h2>

Let’s do <sup>R </sup>4<em>x</em><sup>3</sup><em>dx</em>. Then let’s do to see if we can get 4<em>x</em><sup>3 </sup>back.

def test_07():

print(’
***** Test 07 ***********’) fex = make_prod(make_const(4.0), make_pwr(’x’, 3.0)) print(fex) afex = antideriv(fex)

assert not afex is None print(afex) fexf = tof(fex) assert not fexf is None fex2 = deriv(afex) assert not fex2 is None print(fex2) fex2f = tof(fex2) assert not fex2f is None err = 0.0001 for i in range(11):

assert abs(fexf(i) – fex2f(i)) &lt;= err

print(’Test 07: pass’)

Here is the output of test_07 in the Py shell.

***** Test 07 ***********

(4.0*(x^3.0))

((4.0*(((1.0/4.0)*(x^4.0))+0.0))+0.0)

((4.0*((((1.0/4.0)*(4.0*(x^3.0)))+((x^4.0)*0.0))+0.0))+0.0)

Test 07: pass

<h2>Test 08</h2>

Let’s do <sup>R </sup>(5<em>x </em>− 7)<sup>−2</sup><em>dx</em>. In addition to comparing the antiderivative with the ground truth, let’s convertto a function and see if that function agrees with (5<em>x </em>− 7)<sup>−2 </sup>on a range of values.

def test_08():

print(’
***** Test 08 ***********’) fex1 = make_plus(make_prod(make_const(5.0), make_pwr(’x’, 1.0)),

make_const(-7.0))

fex = make_pwr_expr(fex1, -2.0) print(fex) afex = antideriv(fex) assert not afex is None print(afex) afexf = tof(afex) err = 0.0001 def gt(x):

return (-1.0/5.0)*((5*x – 7.0)**-1)

for i in range(1, 100):

assert abs(afexf(i) – gt(i)) &lt;= err

fexf = tof(fex) assert not fexf is None fex2 = deriv(afex) assert not fex2 is None print(fex2) fex2f = tof(fex2) assert not fex2f is None for i in range(1, 100):

assert abs(fexf(i) – fex2f(i)) &lt;= err

print(’Test 08: pass’)

Here is the output of test_08 in the Py shell.

***** Test 08 ***********

(((5.0*(x^1.0))+-7.0)^-2.0)

(-0.2*(((5.0*(x^1.0))+-7.0)^-1.0))

(-0.2*((-1.0*(((5.0*(x^1.0))+-7.0)^-2.0))*

((5.0*(1.0*(x^0.0)))+0.0)))

Test 08: pass

<h2>Test 09</h2>

Let’s do.

def test_09():

print(’
***** Test 09 ***********’) fex0 = make_plus(make_pwr(’x’, 1.0), make_const(2.0)) fex1 = make_pwr_expr(fex0, -1.0) fex = make_prod(make_const(3.0), fex1) print(fex) afex = antideriv(fex) err = 0.0001 afexf = tof(afex) def gt(x):

return 3.0*math.log(abs(2.0 + x), math.e)

for i in range(1, 101):

assert abs(afexf(i) – gt(i)) &lt;= err

assert not afex is None print(afex) fexf = tof(fex) assert not fexf is None fex2 = deriv(afex) assert not fex2 is None print(fex2)

fex2f = tof(fex2) assert not fex2f is None for i in range(1, 1000):

assert abs(fexf(i) – fex2f(i)) &lt;= err

print(’Test 09: pass’)

Here is the output of test_09 in the Py shell.

***** Test 09 ***********

3.0*(((x^1.0)+2.0)^-1.0))

((3.0*(1.0*ln|((x^1.0)+2.0)|))+0.0)

((3.0*(1.0*((((x^1.0)+2.0)^-1.0)*((1.0*(x^0.0))+0.0))))+0.0)

Test 09: pass

<h2>Test 10</h2>

Let’s do <sup>R </sup>(3<em>x </em>+ 2)<sup>4 </sup><em>dx</em>.

def test_10():

print(’
***** Test 10 ***********’) fex0 = make_prod(make_const(3.0), make_pwr(’x’, 1.0)) fex1 = make_plus(fex0, make_const(2.0)) fex = make_pwr_expr(fex1, 4.0) print(fex) afex = antideriv(fex) assert not afex is None print(afex) afexf = tof(afex) err = 0.0001 def gt(x):

return (1.0/15)*((3*x + 2.0)**5)

for i in range(1, 10):

assert abs(afexf(i) – gt(i)) &lt;= err

fexf = tof(fex) assert not fexf is None fex2 = deriv(afex) assert not fex2 is None print(fex2) fex2f = tof(fex2) assert not fex2f is None for i in range(1, 1000): print(’Test 10: pass’) Here is the output of test_10 in the Py shell. ***** Test 10 ***********

(((3.0*(x^1.0))+2.0)^4.0)

(0.0666666666667*(((3.0*(x^1.0))+2.0)^5.0))

(0.0666666666667*((5.0*(((3.0*(x^1.0))+2.0)^4.0))*

((3.0*(1.0*(x^0.0)))+0.0)))

Test 10: pass

<h1>Problem 2: Splitting, Merging, and Amplifying Images</h1>

This problem will kick off our journey into OpenCV. The primary objective is to ensure that your installation of OpenCV is up and running.

The archive hw07.zip contains the folder images with 50 images of roads and highways in Cache Valley. Let’s call the extension of an image file (e.g., .jpg) a file type or ftype. Write the function read_img_dir(ftype, imgdir) that takes two strings, ftype and imgdir, and returns a list of 2-tuples such that the first element of each 2-tuple of a path to an image of a given ftype in the directory imgdir and the second element is the 2D numpy matrix of that image. For example, the ftype can be ’.jpg’ or ’.png’).

When you work on this function you will likely need to traverse a directory and return the absolute path names to each file that ends in a given extension (i.e., ftype). Here is one way of doing it with a Python generator. There are other ways of listing files in a directory in Python, but I prefer to use generators, because they are more memory efficient, which allows one to process terrabytes of data.

def generate_file_names(ftype, rootdir):

’’’ recursively walk dir tree beginning from rootdir and generate full paths to all files that end with ftype.

sample call: generate_file_names(’.jpg’, /home/pi/images/’)

’’’ for path, dirlist, filelist in os.walk(rootdir): for file_name in filelist:

if not file_name.startswith(’.’) and  file_name.endswith(ftype):

yield os.path.join(path, file_name)

for d in dirlist: generate_file_names(ftype, d)

Let’s test this function.

&gt;&gt;&gt; imglist = read_img_dir(’.jpg’, ’/home/pi/images/’)

&gt;&gt;&gt; len(imglist)

50

Below we see that the first element of the first 2-tuple is an image path and the second is a 2D numpy array corresponding to the image saved in the specified path.

&gt;&gt;&gt; imglist[0][0]

’/home/pi/images/output14889.jpg’

&gt;&gt;&gt; imglist[0][1] array([[[ 78, 140, 150], [ 62, 127, 136],

[ 55, 124, 134], …,

[ 87, 137, 149],

[ 89, 139, 151],

[ 89, 139, 151]]], dtype=uint8)

Here is how we can test the dimensions of the first image.

&gt;&gt;&gt; imglist[0][1].shape (1080, 1920, 3)

So, it is a 1080 by 1920 image with 3 channels.

Write the function grayscale(i, imglist) that an integer <em>i </em>and a list of 2tuples returned by read_img_dir and shows two image windows. The first image window shows the i-th image (i.e., the 2D numpy matrix of the i-th 2tuple in imglist). The title of the first window is the full path to the image (i.e., the first element of the i-th 2-tuple). The second image window shows the grayscaled version of the 2D numpy matrix. The title of that window should read “Grayscaled.” These are pretty big images so, depending on the size of your screen, you may be able to see only parts of the windows.

Save your implementation in hw07_s19.py

Write the function split_merge(i, imglist) that takes the same arguments as grayscale. This function splits the image in the i-th 2-tuple in imglist into the blue, green, and red channels, and then displays each channel in a separate window along with the window with the original image. The title of the window with the original image is the image path. The red channel is displayed in the window whose title is “Red,” the blue channel – in the window whose title is “Blue,” and the green channel – in the window whose title is “Green.” Each window should display the image not in grayscale but in the corresponding color, i.e., red, green, and blue.

Save your implementation in hw07_s19.py

Write the function amplify(i, imglist, c, amount). The first two arguments are the same as in grayscale and split_merge. The third argument, c, is a string whose value is ’b’, ’g’, or ’r’. This argument specifies the channel. The fourth argument, amount, is an integer that gives the amount of amplification with which the channel c will be amplified. This function displays two windows. The first window displays the image in the i-th tuple of imglist. The title of the first window is the full path to the image. The second window displays the amplified image. The title of the second window is “Amplified.”

Save your implementation in hw07_s19.py