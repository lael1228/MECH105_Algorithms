This algorithm filters out the outliers of data and creates a linear regression equation.
- Compute interquartile ranges
- Sort x and y
- Discard the outliers
- Determine R-squared value (coefficient of determination)
- Compute the mean, total sum of the squares, and total sum of squares of residuals

Inputs
- x-values of the data set
- y-values of the data set

Outputs
- Filtered x-values (i.e. the input x-values but without the outlier points), sorted from smallest to largest
- Filtered y-valeus (i.e. the input y-values but without the outlier points), sorted from smallest to largest
- Slope from the linear regression (m in f(x)=mx+b)
- Intercept from the linear regression (b in f(x)=mx+b)
- Rsquared value

function [fX, fY, slope, intercept, Rsquared] = linearRegression(x,y)

% Lael Niemann

%linearRegression Computes the linear regression of a data set

[sortedY, sortOrder] = sort(y);

sortedX = x(sortOrder)

n = length(x);

k = true(1,n);

if length(x)~=length(y)

        error('inputs not =')
        
end

Q1 = quantile(sortedY,0.25)

Q3 = quantile(sortedY,0.75)

%Q1 = ((sortedY+1)/4)

%Q3 = ((3*sortedY+3)/4)

IQR = Q3 - Q1;

for i=1:n

    if Q3+IQR*1.5 < sortedY(i) && Q1-IQR*1.5 < sortedY(i)
    
        k(i) = 0
        
    end
    
    if sortedY(i) == 0
    
        k(i) = 0
        
    end
    
end


fX = sortedX(k);

fY = sortedY(k);

fn = length(fY);

sum_y = sum(fY);

sum_x = sum(fX);

average_y = sum_y./fn;

average_x = sum_x./fn;

sum_x2 = sum(fX.^2);

sum2_x2 = (sum_x).^2;

sum_xy = sum(fX.*fY);

slope = ((fn*sum_xy)-(sum_x*sum_y))./((fn*sum_x2)-(sum2_x2));

intercept = average_y - slope*average_x;

linearRegression = slope*fX + intercept;

SS_t = sum((fY-average_y).^2);

SS_r = sum((fY-linearRegression).^2);

Rsquared = 1-(SS_r/SS_t);

end
