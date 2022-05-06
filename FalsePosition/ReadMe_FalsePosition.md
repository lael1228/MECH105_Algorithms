This algorithm estimates the root of a given function. The algorithm should include:

Inputs
  -   func - the function being evaluated
  -    the lower guess
  -   the upper guess
  -   es - the desired relative error (should default to 0.0001%)
  -   maxit - the maximum number of iterations to use (should default to 200)
  -   varargin, . . . - any additional parameters used by the function

Outputs
  -   root - the estimated root location
  -   fx - the function evaluated at the root location
  -   ea - the approximate relative error (%)
  -   iter - how many iterations were performed


function [root, fx, ea, iter] = falsePosition(func, xl, xu, es, maxit, varargin)

%falsePosition finds the root of a function using false position method

fxl = func(xl,varargin {:})

fxu = func(xu,varargin {:})

if nargin < 3

    error('not enough inputs');
    
end

if fxl*fxu > 0

    error('inputs same sign, not bracketed');
    
end

iter = 0;

maxit = 200;

es = 0.0001;

ea = 100;

while (1)

    root = xu-(fxu*(xl-xu))./(fxl-fxu);
    
    fxr = func(root,varargin {:});
    
    iter = iter+1;
    
    x_old = root
    
    if fxr == 0
    
        root = root; 
        
        ea = 0
        
    else fxr ~= 0
    
        if fxr > 0 
        
            ea = abs((xu-x_old)/xu)*100
            
            xu = root;
            
        else fxr < 0 
        
            ea = abs((xl-x_old)/xl)*100
            
            xl = root;
            
        end
        
    end
    
        if iter>=maxit||ea<=es
        
            break
            
        end
        
    end
    
    fx = func(root,varargin {:})
    
    root = root
    
    iter = iter
    
    ea = ea
    
end
