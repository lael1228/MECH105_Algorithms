This algorithm integrates experimental data using Simpson's 1/3 rule.
- Checks for an odd number of intervals
- Also uses trapezoidal rule
- Error check that the inputs are the same length.
- Error check that the x input is equally spaced.
- Warn the user (not an error, just a warning) if the trapezoidal rule has to be used on the last interval.

function [I] = Simpson(x, y)

% Numerical evaluation of integral by Simpson's 1/3 Rule

% Inputs

%   x = the vector of equally spaced independent variable

%   y = the vector of function values with respect to x

% Outputs:

%   I = the numerical integral calculated

sizex = size(x)

sizey = size(y)

xmax = x(1,end)

xmin = x(1,1)

ymax = y(1,end)

ymin = y(1,1)

n = x(:)

I = 0

i = 1

while (1) 

    i = i+1
    
    h = (xmax-xmin)./(sizey(2)-1)
    
    if length(x)~=length(y)
    
        error('inputs not =')
        
    end
    
    if range(x(2:end)-x(1:end-1))~=0
    
        error('x values not uniform')
        
    end
    
    if sizey(2)==2
    
        warning('trapezoid rule')
        
        I=h.*((ymin+ymax)./2)
        
        break
        
    elseif sizey(2)==3
    
        y(2) = 4.*y(2)
        
        ysum = sum(y(:))
        
        I = (h./3).*(ysum)
        
        break
        
    else sizey(2)>3
    
        if i==(sizex(2)-1)
        
            if mod(sizex(2),2)==0
            
                warning('trapezoid rule due to odd value')
                
                ysum = sum(y(:))-ymax
                
                I = (h/3)*(ysum)+(h./2)*(y(sizex(2)))+(y(sizex(2)-1));
                
                break
                
            else mod(sizex(2),2)==1
            
                ysum=sum(y(:))
                
                I = (h./3).*(ysum)
                
                break
                
            end
            
        elseif mod(i,2)==1
        
            y(i)=2*y(i)
            
        else mod(i,2)==0
        
            y(i)=4*y(i)
            
        end
        
    end
    
end

I=I

end
