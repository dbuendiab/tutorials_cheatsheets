<strong>

I just went through some pain (again) when I wanted to install some of Python's scientific libraries on my second Mac. I summarized the setup and installation process for future reference.<br/>
If you encounter any different or additional obstacles let me know, and please feel free to make any suggestions to improve this short walkthrough.
 </strong></p></div>


<br>
<br>
<p><img src="../Images/python_sci_pack_ing.png" alt="" /></p>

<hr>


<h4>Sections</h4>

<p>&#8226; <a href="#conda">Anaconda and Miniconda</a><br>
&#8226; <a href="#venv">Consider a virtual environment</a><br>
&#8226; <a href="#pip">Installing pip</a><br>
&#8226; <a href="#numpy">Installing NumPy</a><br>
&#8226; <a href="#scipy">Installing SciPy</a><br>
&#8226; <a href="#matplotlib">Installing matplotlib</a><br>
&#8226; <a href="#ipython">Installing IPython</a><br>
&#8226; <a href="#updating">Updating installed packages</a><br></p>

<p><br></p>

<hr>


<p><br></p>

<p><a name="conda"></a>
<br>
<br></p>

<h2>Anaconda and Miniconda</h2>

<p><br></p>

<p>Alternatively, instead of going through all the manual steps listed in the following sections, there is the <a href="https://store.continuum.io/cshop/anaconda/">Anaconda Python distribution</a> for scientific computing. Although Anaconda is distributed by Continuum Analytics, it is completely free and includes more than 125 packages for science and data analysis.<br/>
The installation procedure is nicely summarized here: <a href="http://docs.continuum.io/anaconda/install.html">http://docs.continuum.io/anaconda/install.html</a></p>

<p>If this is too much, the <a href="http://repo.continuum.io/miniconda/">Miniconda</a> might be right for you. Miniconda is basically just a Python distribution with the Conda package manager, which let's us install a list of Python packages into a specified conda environment.</p>

<div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #996633">$[</span>bash<span style="color: #333333">]</span>&gt; conda create -n myenv <span style="color: #996633">python</span><span style="color: #333333">=</span>3
<span style="color: #996633">$[</span>bash<span style="color: #333333">]</span>&gt; conda install -n myenv numpy scipy matplotlib ipython
</pre></div>


<p>Note: environments will be created in <code>ROOT_DIR/envs</code> by default, you can use the <code>-p</code> instead of the <code>-n</code> flag in the conda commands above in order to specify a custom path.</p>

<p>If you we decided pro Anaconda or Miniconda, we are basically done at this point. The following sections are explaining a more (semi)-manual approach to install the packages individually using <code>pip</code>.</p>

<p><a name="venv"></a>
<br>
<br></p>

<h2>Consider a virtual environment</h2>

<p><br>
In order to not mess around with our system packages, we should consider setting up a virtual environment when we want to install the additional scientific packages. <br/>
To set up a new virtual environment, we can use the following command</p>

<div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #996633">$[</span>bash<span style="color: #333333">]</span>&gt; python3 -m venv /path_to/my_virtual_env
</pre></div>

<p>and activate it via</p>

<div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #996633">$[</span>bash<span style="color: #333333">]</span>&gt; <span style="color: #007020">source</span> /path_to/my_virtual_env/bin/activate
</pre></div>


<p><a name="pip"></a>
<br>
<br></p>

<h2>Installing pip</h2>

<p><br>
<code>pip</code> is a tool for installing and managing Python packages. It makes the installation process for Python packages a lot easier, since they don't have to be downloaded manually.<br/>
If you haven't installed the <code>pip</code> package for your version of Python, yet, I'd suggest to download it from <a href="https://pypi.python.org/pypi/pip">https://pypi.python.org/pypi/pip</a>, unzip it, and install it from the unzipped directory via</p>

<div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #996633">$[</span>bash<span style="color: #333333">]</span>&gt; python3 setup.py install
</pre></div>

<p><a name="numpy"></a>
<br>
<br></p>

<h2>Installing NumPy</h2>

<p><br>
Installing NumPy should be straight forward now using <code>pip</code></p>

<div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #996633">$[</span>bash<span style="color: #333333">]</span>&gt; python3 -m pip install numpy
</pre></div>



<p>The installation will probably take a few minutes due to the source files that have to be compiled for your machine. Once it is installed, <code>NumPy</code> should be available in Python via</p>

<div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #888888">&gt;&gt; import numpy</span>
</pre></div>

<p>If you want to see a few examples of how to operate with NumPy arrays, you can check out my <a href="http://sebastianraschka.com/Articles/2014_matlab_vs_numpy.html">Matrix Cheatsheet for Moving from MATLAB matrices to NumPy arrays</a></p>

<p><a name="scipy"></a>
<br>
<br></p>

<h2>Installing SciPy</h2>

<p><br>
While the <code>clang</code> compiler worked fine for compiling the C source code for <code>numpy</code>, we now need an additional Fortran compiler in order to install <code>scipy</code>.</p>

<p><br></p>

<h4>Installing a Fortran Compiler</h4>

<p>Unfortunately, MacOS 10.9 Mavericks doesn't come with a Fortran compiler, but it is pretty easy to download and install one.<br/>
For example, <code>gfortran</code> for MacOS 10.9 can be downloaded from <a href="http://coudert.name/software/gfortran-4.8.2-Mavericks.dmg">http://coudert.name/software/gfortran-4.8.2-Mavericks.dmg</a></p>

<p>Just double-click on the downloaded .DMG container and follow the familiar MacOS X installation procedure. Once it is installed, the <code>gfortran</code> compiler should be available from the command line,. We can test it by typing</p>

<div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #996633">$[</span>bash<span style="color: #333333">]</span>&gt; gfortran -v
</pre></div>


<p>Among other information, we will see the current version, e.g.,</p>

<pre>gcc version 4.8.2 (GCC)</pre>


<p><br></p>

<h4>Installing SciPy</h4>

<p>Now, we should be good to go to install <code>SciPy</code> using <code>pip</code>.</p>

<div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #996633">$[</span>bash<span style="color: #333333">]</span>&gt; python3 -m pip install scipy
</pre></div>


<p>After it was successfully installed - might also take a couple of minutes due to the source code compilation - it should be available in Python via</p>

<div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #888888">&gt;&gt; import scipy</span>
</pre></div>

<p><a name="matplotlib"></a>
<br>
<br></p>

<h2>Installing matplotlib</h2>

<p><br>
The installation process for matplotlib should go very smoothly using <code>pip</code>, I haven't encountered any hurdles here.</p>

<div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #996633">$[</span>bash<span style="color: #333333">]</span>&gt; python3 -m pip install matplotlib
</pre></div>


<p>After successful installation, it can be imported in Python via</p>

<div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #888888">&gt;&gt; import matplotlib</span>
</pre></div>

<p>The <code>matplotlib</code> library has become my favorite data plotting tool recently, you can check out some examples in my little matplotlib-gallery on GitHub: <a href="https://github.com/rasbt/matplotlib_gallery">https://github.com/rasbt/matplotlib_gallery</a></p>

<p><a name="ipython"></a>
<br>
<br></p>

<h2>Installing IPython</h2>

<p><br></p>

<h4>Installing pyzmq</h4>

<p>The IPython kernel requires the <code>pyzmq</code> package to run, <code>pyzmq</code> contains Python bindings for ØMQ, which is a lightweight and fast messaging implementation. It can be installed via <code>pip</code>.</p>

<div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #996633">$[</span>bash<span style="color: #333333">]</span>&gt; python3 -m pip install pyzmq
</pre></div>

<p><br></p>

<h4>Installing pyside</h4>

<p>When I was trying to install the <code>pyside</code> package, I had it complaining about the missing <code>cmake</code>. It can be downloaded from:</p>

<p><a href="http://www.cmake.org/files/v2.8/cmake-2.8.12.2-Darwin64-universal.dmg">http://www.cmake.org/files/v2.8/cmake-2.8.12.2-Darwin64-universal.dmg</a></p>

<p>Just as we did with <code>gfortran</code> in the <a href="#scipy">Installing SciPy section</a>, double-click on the downloaded .DMG container and follow the familiar MacOS X installation procedure.<br/>
We can confirm that it was successfully installed by typing</p>

<div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #996633">$[</span>bash<span style="color: #333333">]</span>&gt; cmake --version
</pre></div>


<p>into the command line where it would print something like</p>

<pre>cmake version 2.8.12.2</pre>


<p><br></p>

<h4>Installing IPython</h4>

<p>Now, we should finally be able to install IPython with all its further dependencies (pygments, Sphinx, jinja2, docutils, markupsafe) via</p>

<div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #996633">$[</span>bash<span style="color: #333333">]</span>&gt; python3 -m pip install ipython<span style="color: #333333">[</span>all<span style="color: #333333">]</span>
</pre></div>

<p>By doing this, we would install IPython to a custom location, e.g., <code>/Library/Frameworks/Python.framework/Versions/3.3/lib/python3.3/site-packages/IPython</code>.</p>

<p>You can find the path to this location by importing IPython in Python and then print its path:</p>

<div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #888888">&gt;&gt; import IPython</span>
<span style="color: #888888">&gt;&gt; IPython.__path__</span>
</pre></div>

<p>Finally, we can set an <code>alias</code> in our <code>.bash_profile</code> or <code>.bash_rc</code> file to conviniently run IPython from the console. E.g.,</p>

<pre>alias ipython3="python3 /Library/Frameworks/Python.framework/Versions/3.3/lib/python3.3/site-packages/IPython/terminal/ipapp.py"</pre>


<p>(Don't forget to <code>source</code> the <code>.bash_rc</code> or <code>.bash_profile</code> file afterwards)</p>

<p>Now we can run</p>

<div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #996633">$[</span>bash<span style="color: #333333">]</span>&gt; ipython3
</pre></div>

<p>from you shell terminal to launch the interactive IPython shell, and</p>

<div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #996633">$[</span>bash<span style="color: #333333">]</span>&gt; ipython3 notebook
</pre></div>

<p>to bring up the awesome IPython notebook in our browser, respectively.</p>

<p><a name="updating"></a>
<br>
<br></p>

<h2>Updating installed packages</h2>

<p><br>
Finally, if we want to keep our freshly installed packages up to date, we'd run <code>pip</code> with the <code>--upgrade</code> flag, for example</p>

<div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #996633">$[</span>bash<span style="color: #333333">]</span>&gt; python3 -m pip install numpy --upgrade 
</pre></div>