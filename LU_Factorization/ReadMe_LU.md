This algorithm determines the LU Factorization of a square matrix.
- It must use partial pivoting
- Must include errors

Inputs
- A - coefficient matrix

Outputs
- L - lower triangular matrix, with 1's along the diagonals
- U - upper triangular matrix
- P - the pivot matrix

% a correctly solved LU factorization solves for the problem P*A = L*U

function [L, U, P] = luFactor(A)

% luFactor(A)

%	LU decomposition with pivotiing

% inputs:

%	A = coefficient matrix

% outputs:

%	L = lower triangular matrix

%	U = upper triangular matrix

%       P = the permutation matrix

dim = length(A);

L = zeros(dim);

U = zeros(dim);

P = eye(dim);

for i=1:dim

    if size(L)~=size(A)
    
            error('matrix is singular')
            
            U = NaN;
            
            L = NaN;
            
            return
            
end

[~,r] = max(abs(A(i:end,i)));

r = dim-(dim-i+1)+r;

A([i,r],:) = A([r,i],:);

P([i,r],:) = P([r,i],:);

L([i,r],:) = L([r,i],:);

L(i:dim,i) = A(i:dim,i) / A(i,i);
    
U(i,1:dim) = A(i,1:dim);

A(i+1:dim,1:dim) = A(i+1:dim,1:dim) - L(i+1:dim,i)*A(i,1:dim);

end

U(:,end) = A(:,end);

end
