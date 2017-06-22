---
title: Python Decorators
date: 2016-05-20 21:15:37
tags: Python Decorator
categories: Programming Languages
---
# Python Decorators Overview
from [pythoncentral.io](http://pythoncentral.io/python-decorators-overview/), and [thecodeship.com](http://thecodeship.com/patterns/guide-to-python-function-decorators/)  
## Decorator  
Function decorators are simply wrappers to existing functions. In this example let's consider a function that wraps the string output of another function by p tags.		
		def get_text(name):
		   return "lorem ipsum, {0} dolor sit amet".format(name)
		
		def p_decorate(func):
		   def func_wrapper(name):
		       return "<p>{0}</p>".format(func(name))
		   return func_wrapper
		
		my_get_text = p_decorate(get_text)
		
		print my_get_text("John")  
That was our first decorator. A function that takes another function as an argument, generates a new function, augmenting the work of the original function, and returning the generated function so we can use it anywhere.  
In Python, we can use "@" to do the same thing.  
  
		def p_decorate(func):
		   def func_wrapper(name):
		       return "<p>{0}</p>".format(func(name))
		   return func_wrapper
		
		@p_decorate
		def get_text(name):
		   return "lorem ipsum, {0} dolor sit amet".format(name)
		
		print get_text("John")
		
		# Outputs <p>lorem ipsum, John dolor sit amet</p>  
  
Now let's consider we wanted to decorate our get_text function by 2 other functions to wrap a div and strong tag around the string output.    

		def p_decorate(func):
		   def func_wrapper(name):
		       return "<p>{0}</p>".format(func(name))
		   return func_wrapper
		
		def strong_decorate(func):
		    def func_wrapper(name):
		        return "<strong>{0}</strong>".format(func(name))
		    return func_wrapper
		
		def div_decorate(func):
		    def func_wrapper(name):
		        return "<div>{0}</div>".format(func(name))
		    return func_wrapper  
With the basic approach, decorating get_text would be along the lines of    

		get_text = div_decorate(p_decorate(strong_decorate(get_text)))  
With Python's decorator syntax, same thing can be achieved with much more expressive power.    

		@div_decorate
		@p_decorate
		@strong_decorate
		def get_text(name):
		   return "lorem ipsum, {0} dolor sit amet".format(name)
		
		print get_text("John")
		
		# Outputs <div><p><strong>lorem ipsum, John dolor sit amet</strong></p></div>