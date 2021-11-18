# SimpleLinearRegression
Simple linear regression examples.
---
title: "Regressão Linear Simples"
subtitle: "Distribuição Beta"
author: "Gleyce Alves Pereira da Silva"

output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
<br/><br/>

<center> <h1> 
</h2> </center>

<br/><br/>

<center> <h2> Distribuição Beta
</h2> </center>

# Distribuição Beta

<p> Seja $X \sim Beta(a,b)$, temos que a densidade da distribuição Beta é da forma:

\begin{equation}
f(x; a, b) = \dfrac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)} x^{a-1}(1-x)^{b-1} \hspace{0.2cm}, 0<x<1; a,b>0
\end{equation}<p>

A distribuição Beta possui dois parâmetros, $a$ e $b$, que   determinam a forma das distribuições Beta (assim como a média e a variância determinam a forma da distribuição normal).

<p> Vamos simular um conjunto de dados com uma amostra de tamanho $n=100$. 


<p>	

```{r}
set.seed(041196)
y <- rbeta(100, 1, 2)
```
<br/><br/>
<center> <h2> Histograma </h2> </center>

<p> 	Com intermédio da linguagem R, foram construídos histogramas para a amostra obtida com a função \textit{rbeta} para alguns valores de $a$ e $b$ com $n=100$ fixo para ambas as amostras.
	Analisamos três casos distintos: $a=b, a<b$ e $a>b$.<p>
	
###  Histograma para $a=b$

```{r}
set.seed(041196)
y <- rbeta(100, 2, 2)
hist(y, prob = TRUE, main= "Histograma da Distribuição Beta, a=b.", 
     xlab = "Dados gerados", ylab= "P[X = x]", col="aquamarine")
lines(density(y), col="blue", lwd=2) #estimativa de densidade beta
lines(density(y, adjust=2), lty="dotted", col="darkgreen", lwd=2) 
```

###  Histograma para $a<b$
```{r}
set.seed(041196)
y <- rbeta(100, 1, 2) #cria uma sequencia aleatoria de numeros com distribuição beta 
hist(y, prob = TRUE, main= "Histograma da Distribuição Beta, a<b.", 
     xlab = "Dados gerados", ylab= "P[X = x]", col="aquamarine")
lines(density(y), col="blue", lwd=2) #estimativa de densidade beta
lines(density(y, adjust=2), lty="dotted", col="darkgreen", lwd=2) 
```



###  Histograma para $a>b$
```{r}
set.seed(041196)
y <- rbeta(100, 2, 1)
hist(y, prob = TRUE, main= "Histograma da Distribuição Beta, a>b.", 
     xlab = "Dados gerados", ylab= "P[X = x]", col="aquamarine")
lines(density(y), col="blue", lwd=2) #estimativa de densidade beta
lines(density(y, adjust=2), lty="dotted", col="darkgreen", lwd=2) 
```
<br/><br/>
<center> <h2> Gráfico da densidade da distribuição Beta para diversos parâmetros </h2> </center>


### Caso 1: $a=b$ e $a,b \geq 1$
```{r}
p = seq(0,1, length=100)
plot(p, dbeta(p, 100, 100), ylab="Densidade", type ="l", col=4)
lines(p, dbeta(p, 10, 10), type ="l", col=3)
lines(p, dbeta(p, 2, 2), col=2) 
lines(p, dbeta(p, 1, 1), col=1) 
legend(0.7,8, c("Beta(100,100)","Beta(10,10)","Beta(2,2)", "Beta(1,1)"),lty=c(1,1,1,1),col=c(4,3,2,1))
```

###  Caso 2: $a \neq b$ e $a,b \geq 1$
```{r}
p = seq(0,1, length=100)
plot(p, dbeta(p, 900, 100), ylab="Densidade", type ="l", col=4)
lines(p, dbeta(p, 90, 10), type ="l", col=3)
lines(p, dbeta(p, 30, 70), col=2) 
legend(0.2,30, c("Beta(900,100)","Beta(90,10)","Beta(30,70)", "Beta(3,7)"),lty=c(1,1,1,1),col=c(4,3,2,1))

```

###  Caso 3: $a,b <1$
```{r}
p = seq(0,1, length=100)
plot(p, dbeta(p, 0.1, 0.1), ylim=c(0,3),ylab="Densidade", type ="l", col=4)
lines(p, dbeta(p, 0.5, 0.5), type ="l", col=3)
lines(p, dbeta(p, 0.1, 0.5), col=2) 
lines(p, dbeta(p, 0.5, 2), col=1) 
legend(0.5,2, c("Beta(0.1,0.1)","Beta(0.5,0.5)","Beta(0.1,0.5)", "Beta(0.5,2)"),lty=c(1,1,1,1),col=c(4,3,2,1))
```

###  Caso 4: $a,b =1$
```{r}
p = seq(0,1, length=100)
plot(p, dbeta(p, 1, 1), ylim=c(0,3),ylab="Densidade", type ="l", col=4)
lines(p, dbeta(p, 1, 1), type ="l", col=3)
lines(p, dbeta(p, 1, 1), col=2) 
lines(p, dbeta(p, 1, 1), col=1) 
lines(p, dbeta(p, 1, 1), col=1) 
```
<p> Sejam $y_1, y_2,...,y_n$ variáveis aleatórias indenticamente distribuídas de uma distribuição Beta de parâmetros $a$ e $b \in \mathbb{R}_{+}$. Sendo $n$ amostras independentes a *função de verossimilhança* tem a seguinte forma: <p>


\begin{equation}
L(\theta |\mathbf{y}) = \prod_{i=1}^{n}\dfrac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)} y_{i}^{a-1}(1-y_i)^{b-1}

\end{equation}

como cada observação é independente, temos:

\begin{equation}
L(\theta |\mathbf{y}) = \left[\dfrac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)} \right]^{n} \left[\sum_{i=1}^{n} y_i\right]^{a-1} \left[\sum_{i=1}^{n} 1 - y_i\right]^{b-1}
\end{equation}

Agora, vamos encontrar a *função de log-verossimilhança* $l(\theta |\mathbf{y})$.

\begin{equation}
l(\theta |\mathbf{y}) = nln(\Gamma(a+b)) - nln(\Gamma(a)) - nln(\Gamma(b)) + (a-1)\sum_{i=1} ^{n}ln(y_i) +  (b-1)\sum_{i=1} ^{n}ln(1 - y_i).
\end{equation}

A função escore é obtida derivando a função $l(\theta|\mathbf{y})$ com respeito a $a$ e $b$, respectivamente,

\begin{equation}
S(a) = \dfrac{\partial }{\partial a}l(\theta |\mathbf{y}) = n \dfrac{\Gamma'(a,b)}{\Gamma(a,b)} - n \dfrac{\Gamma'(a)}{\Gamma(a)} + \sum_{i=1} ^{n}ln(y_i)
\end{equation}

onde $\psi(y) = \dfrac{\Gamma'(y)}{\Gamma(y)}$ é a função digamma. Logo,

\begin{equation}
 S(a) = \psi(a,b) - \psi(a) + \dfrac{1}{n}\sum_{i=1} ^{n}ln(y_i)
\end{equation}

com respeito a $b$, temos:

\begin{equation}
S(b) = \dfrac{\partial }{\partial b}l(\theta |\mathbf{y}) = n \dfrac{\Gamma'(a,b)}{\Gamma(a,b)} - n \dfrac{\Gamma'(b)}{\Gamma(a)} + \sum_{i=1} ^{n}ln(1 - y_i)
\end{equation}

onde $\psi(x) = \dfrac{\Gamma'(x)}{\Gamma(x)}$ é a função digamma. Logo,

\begin{equation}
  S(b)= \psi(a,b) - \psi(b) + \dfrac{1}{n}\sum_{i=1} ^{n}ln(1 - y_i)
\end{equation}

Igualando ambas as derivadas à zero e construindo o sistema, temos:

\begin{cases}
S(a) = \psi(a,b) - \psi(a) + \dfrac{1}{n}\sum_{i=1}^{n}ln(y_i) = 0\\
S(b) = \psi(a,b) - \psi(b) + \dfrac{1}{n}\sum_{i=1}^{n}ln(1 - y_i) = 0 
\end{cases}

Não é possível explicitar, de forma analítica, a raiz do sistema composto pelas equações acima, se fazendo necessário utilizar métodos de otimização para aproximar o valor da estimativa de máxima verossimilhança, como por exemplo o Método de Newton Raphson. 

Temos a informação observada dada por:

\begin{equation}
K(\widehat{\theta}) = \left[\begin{array}{cc} 
\dfrac{\partial ^2}{\partial a^2}l(\theta |\mathbf{y}) & \dfrac{\partial^2}{\partial ab}l(\theta |\mathbf{y})\\
\dfrac{\partial^2}{\partial ba}l(\theta |\mathbf{y}) & \dfrac{\partial ^2 }{\partial b ^2}l(\theta |\mathbf{y})
\end{array}\right]
\end{equation}
 
onde:

\begin{align}
\dfrac{\partial ^2}{\partial a^2}l(\theta |\mathbf{y}) &= \psi'(a+b) - \psi'(a); \\
\dfrac{\partial^2}{\partial ab}l(\theta |\mathbf{y}) &= \dfrac{\partial^2}{\partial ba}l(\theta |\mathbf{y}) = \psi'(a+b); \\
\dfrac{\partial ^2 }{\partial b ^2}l(\theta |\mathbf{y}) &= \psi'(a+b) - \psi'(b); \\ 
\end{align}


Logo, 

\begin{equation}
K(\theta) = \left[\begin{array}{cc} 
\psi'(a+b) - \psi'(a) & \psi'(a+b) \\
\psi'(a+b)  & \psi'(a+b) - \psi'(b)
\end{array}\right],
\end{equation}
<p>

<br/><br/>
<center> <h2> Teste de hipóteses </h2> </center>

<p> Definindo $\theta=(a,b)^\top$ como o vetor de parâmetros da distribuição *Beta* $X \sim Beta(a,b)$, temos que as hipóteses dos testes estatísticos são:

\begin{equation}
\mathcal{H_0}: \theta = [a_0, b_0]^\top \hspace{0.5cm} vs. \hspace{0.5cm} \mathcal{H_1}: \theta \neq [a_0, b_0]^\top.
\end{equation}

#### -- A estatística da Razão de Verossimilhança é:
\begin{align*}
\text{RV} &=
2[\ell(\widehat{\theta} | \textbf{y}) - \ell(\widetilde{\theta}_0 | \textbf{y})]
\\&=
2\left[nlog\dfrac{\Gamma(\widehat{a}+\widehat{b})}{\Gamma(a_0 + b_0)}-nlog\dfrac{\Gamma(a_0)}{\Gamma(\widehat{a})}-nlog\dfrac{\Gamma(b_0)}{\Gamma(\widehat{b})}+(\widehat{a} - a_0)\sum_{i=0}^{n}log(y_i)+(\widehat{b} - b_0)\sum_{i=0}^{n}log(1-y_i)
\right].
\end{align*}

#### -- A estatística Wald é dada por:
\begin{align*}
\mathcal{W} &= (\widehat{\theta} - \theta_0)^\top K(\widehat{\theta})^{-1} (\widehat{\theta} - \theta_0)
\end{align*}

em que $K(\widehat{\theta})^{-1}$ é a inversa da matriz de informação observada $p×p$, θˆ é o EMV do parâmetro $\theta$ e $\theta_0$ o valor sob a hipótese nula.

#### -- A estatístia de teste Escore é dada por:
\begin{align*}
\operatorname{E} &= S(\theta_0)^\top 
K^{-1}(\theta_0) S(\theta_0).
\end{align*}

em que $S(\theta) = \dfrac{\partial l(\theta)}{\partial \theta}$ é a função e $K(\theta)$ é a matriz de informação observada.

#### -- Estimar os parâmetros numericamente com o pacote optim e método L-BFGS-B

#### -- Função de log-verossimilhança

```{r}
ll_beta <- function(theta, x){
  ll <- dbeta(x, shape = theta[1], shape2  = theta[2], log = TRUE)
  return(-sum(ll))
} 
```

#### -- Estimar os parâmetros

```{r}
EMV <- optim(par = c(1, 1), fn = ll_beta, method = "L-BFGS-B",x=y)
print(EMV, hessian = TRUE)
```
```{r}
EMV <- as.list(EMV)
EMV1 <- EMV$par[1]
EMV2 <- EMV$par[2]
```
<br/><br/>
<center> <h2> Aplicação dos testes </h2> </center>


Vamos considerar os testes de hipóteses para o vetor de parâmetro $\theta=(a,b)^\top$ da distribuição Beta com dois parâmetros, $X \sim Beta(a,b)$. As hipóteses dos testes estatísticos são:


\begin{equation}
\mathcal{H_0}: \theta = [1, 1.5]^\top \hspace{0.5cm} vs. \hspace{0.5cm} \mathcal{H_1}: \theta \neq [1, 1.5]^\top .
\end{equation}

#### Teste da Razão de Verossimilhança:

```{r}
RV <- function(Est, theta, a, ...){
  VC <- qchisq(1-a, df=length(theta))
  EC <- Est(theta, ...)
  print(ifelse(EC < VC, "Não rejeita H0", "Rejeita H0"))
  return(c(VC, EC))
}

EstRV <- function(theta, x, EMV){
  n <- length(x)
  a <- theta[1]
  b <- theta[2]
  aux1  <- n*(log(gamma(EMV1+EMV2))/(gamma(a+b)))
  aux2  <- n*(log(gamma(a)/gamma(EMV1)))
  aux3   <- n*(log(gamma(b)/gamma(EMV2)))
  aux4 <- (EMV1-a)*(sum(log(x)))
  aux5 <- (EMV2-b)*(sum(log(1-x)))
  lv <- 2*(aux1 - aux2 - aux2 + aux4 +aux5)
  return(lv)
} 


RV(Est = EstRV, theta=c(1, 1.5), EMV=EMV$par, a = 0.05, x=y)
```

#### Teste de Wald para distribuição de probabilidade com mais de um parâmetro:

```{r}

#### --Informação observada
IOW <- function(theta, x){
  n     <- length(x)
  a <- theta[1]
  b <- theta[2]
  Iaa   <- trigamma(a+b) - trigamma(a)
  Ibb   <- trigamma(a+b) - trigamma(b)
  Iab   <- trigamma(a+b)
  I <- matrix(c(Iaa, Iab, Iab, Ibb), nrow=2, ncol=2, byrow = TRUE)
  return(I)
}

#### -- Informação observada com respeito ao parâmetro $a$ usando o $\widehat{b}$ para $b$


IOWa <- function(theta,x){
  n     <- length(x)
  a <- theta[1]
  b  <- theta[2]
  Iaa   <- trigamma(a+b) - trigamma(a)
  return(-Iaa)
}

Wald2 <- function(theta, EMV, IO, a, ...){
  VC  <- qnorm(1-a/2)
  aux <- EMV - theta
  Tw  <- t(aux)%*%solve(IO(theta=EMV, ...))%*%aux
  if(Tw < 0)  print(ifelse(Tw > -VC, "Não rejeita H0", "Rejeita H0"))
  else  print(ifelse(Tw < VC, "Não rejeita H0", "Rejeita H0"))
  if(Tw < 0) return(c(Tw, -VC))
  else return(c(Tw, VC))
}

Wald2(theta=c(1, 1.5), EMV = EMV$par, IO = IOW, a=0.05, x=y)
```

#### Teste Escore:

```{r}

Escore <- function(theta, S, IF, a, ...){
  VC <- qnorm(1-a/2)
  Te <- S(theta, ...)/sqrt(IF(theta, ...))
  print(ifelse(Te < VC, "Não rejeita H0", "Rejeita H0"))
  return(c(Te, VC))
}

#### --Função escore

FescB <- function(theta, x){
  n     <- length(x)
  a <- theta[1]
  b <- theta[2]
  esco1 <- digamma(a+b) - digamma(a) + (1/n)*(sum(log(x)))
  esco2 <- digamma(a+b) - digamma(b) + (1/n)*(sum(log(1-x)))
  return(c(esco1, esco2))
}

#### -- Função escore com respeito ao parâmetro $a$ usando o $\widehat{b}$ para $b$

FescBeta <- function(theta, x){
  n     <- length(x)
  a <- theta[1]
  b <- theta[2]
  esco1 <- digamma(a+b) - digamma(a) + (1/n)*(sum(log(x)))
  return(-esco1)
}

Escore(theta =  c(1, 1.5), S = FescBeta, IF = IOWa, a=0.05, x=y)
```
#### -- Aplicação dos testes para o parâmetro de forma $a$

Vamos considerar os testes de hipóteses para o vetor de parâmetro de forma $a$ da distribuição Beta com dois parâmetros, $X \sim Beta(a,b)$. As hipóteses dos testes estatísticos são:


\begin{equation}
\mathcal{H_0}: a = a_0 \hspace{0.5cm} vs. \hspace{0.5cm} \mathcal{H_1}: a \neq a_0 .
\end{equation} 

#### -- Teste RV

```{r}
RV(Est = EstRV, theta = c(1, EMV$par[2]), EMV=EMV$par, a = 0.05, x=y)
```

#### -- Teste Wald

```{r}
Wald2(theta = c(1, EMV$par[2]), EMV = EMV$par, IO = IOW, a=0.05, x=y)
```

#### -- Teste Escore

```{r}
Escore(theta =  c(1, EMV2), S = FescBeta, IF = IOWa, a=0.05, x=y)
```
#### -- Intervalo de Confiança

Para obter os intervalos de confiança assintótico basta inverter a matriz de informação observada porque não temos a esperada e pegar os termos em sua diagonal que corresponde a variância de $\widehat{a}$ e $\widehat{b}$.

```{r}

Inf_Obs <- IOW(theta = EMV$par, x=y)
print(Inf_Obs)
```

```{r}
DP   <- sqrt(diag(solve(-Inf_Obs)))
IC_a <- EMV$par[1] + c(-1, 1)*qnorm(1-0.05/2)*DP[1]
IC_b <- EMV$par[2] + c(-1, 1)*qnorm(1-0.05/2)*DP[2]
IC   <- rbind(IC_a, IC_b)
colnames(IC) <- c("2,5%", "97,5%")
print(IC)
```

#### -- Gráfico da função de log-verossimilhança para o parâmetro $a$

#### -- Função de log-verossimilhança

```{r}
ll_Be <- function(a, x){
  ll <- dbeta(x, shape1 = a, shape2 = EMV$par[2], log = TRUE)
  return(sum(ll))
} 
```

#### -- Gerar uma sequência de valores para $a$ e calcular $ℓ(a|\mathbf{y})$ para cada um dos valores

```{r}
alpha_vals <- seq(1, 10, len = 100)
Lalpha <- sapply(alpha_vals, ll_Be, x = y)
```

#### -- Agora temos o gráfico da função de log-verossimilhança com respeito ao parâmetro $a$

```{r}
plot(alpha_vals, Lalpha, type="l", lwd = 3.0, ylab="", xlab="", font =2)
mtext(expression(l(a~"|"~bold(y))), 2, line=2.2, cex=1, font=2)
mtext(expression(a), 1, line=2.5,    cex=1, font=2)
points(EMV$par[1], max(Lalpha), cex = 2, pch =16)
```
