Installation
============

`Website <http://gnu-linux.org>`_ is live. This repository is a backup. Shared for learning only. 

 
|

Steps for Contributors
------------------------

1) Clone this repository and install pelican locally **pip install pelican** 

2) Create a rst file with relevant name in **content** directory. 
   You may use the sample template below to start with

.. code:: rst

	The GNU/Linux                                                                   
	#############                                                                   
                                                                           
	:date: 2014-02-26 10:02                                                         
	:author: Srikant Patnaik                                                        
	:pagetitle: GNU/Linux for all                    
	:keywords: Linux, Installing Linux, Ubuntu, Fedora
	:tags: GNU, Linux, Ubuntu
	:description: GNU/Linux is a free operating system, used worldwide in many commercial applications
	:slug: gnulinux
	
	 What is GNU/Linux
	 -----------------
    	
	And here is the rest of the post

4) Save the file and uncomment ::

	SITEURL = 'http://127.0.0.1:8000/'

   line at the top of **pelicanconf.py** file

5) Run **./develop_server.sh start** to start the development server and **stop** to kill the server

6) You may put your image files inside **content/uploads/2014/04/** and use relative path

7) After you done with local testing, push your **rst** file along with images (if any) 
   to server using instruction provided in **email**


Chain of events to setup website from scratch
---------------------------------------------

#. Install necessary packages. If you feel safe to install site system wide, `virtualenv` packages are optional ::

	sudo apt-get install python-pip python-virtualenv virtualenvwrapper python-dev apache2

#. Setting up `virtualenvwrapper` ::

	echo 'export PROJECT_HOME=~/Documents' >> .bashrc
	echo 'export WORKON_HOME=~/Documents/virtualenvs' >> .bashrc

#. Restart terminal, and create virtualenv ::

	mkproject gnu-linux.org

#. This will drop to ``gnu-linux.org`` virtualenv. Now install `pelican` ::

	pip install pelican 

#. To log the version of installed packages ::

	pip freeze > requirements.txt

#. Now run ``pelican-quickstart`` and follow the on-screen instructions::

	pelican-quickstart

#. Setup `apache`. Add following text in `/etc/apache2/sites-available/gnu-linux.org.conf` ::

	
	<VirtualHost *:80>                                                              
        DocumentRoot /home/srikant/Documents/gnu-linux.org/output/              
        ServerName gnu-linux.org                                                
        ServerAlias www.gnu-linux.org                                           
        <Directory "/home/srikant/Documents/gnu-linux.org/output/">             
            Order allow,deny                                                    
            Allow from all                                                      
            Require all granted                                                 
        </Directory>                                                            
	</VirtualHost>	


#. To test locally, add in `/etc/hosts`::

	127.0.0.1  gnu-linux.org


#. Change the permission of `output` directory to `www-data` ::

	sudo chown -R www-data.www-data /home/srikant/Documents/gnu-linux.org/output/

#. Enable site ::

	sudo a2ensite gnu-linux.org

#. Reload apache configuration ::

	sudo service apache2 reload

#. Optional. Import existing wordpress site using ``pelican-import`` ::

	pelican-import --wpfile -o content ~/Downloads/gnu-linuxorg.wordpress.2014-02-03.xml

#. To generate html files ::

	make html

#. This will create html files in ``output`` directory. 

#. Optional. To install themes in virtualenv, create a `static` directory ::

	mkdir static && cd static 

#. Clone the `pelican theme` repository ::

	git clone https://github.com/getpelican/pelican-themes.git --depth=1


#. To enable theme, just change the name in `pelicanconf.py` file. 

