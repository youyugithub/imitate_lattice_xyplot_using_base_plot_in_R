# imitate_lattice_xyplot_using_base_plot_in_R

imitate_lattice_xyplot_using_base_plot_in_R

How to add titles to each subplot in R


### to put title inside the plot range

```
plot(c(-5,-3),c(-5,-3),type="l")
# title("Title", line = -1)
op<-par("usr");par(usr=c(0,1,0,1))########
rect(0,0.9,1,1,col="gray80")
text(0.5,0.95,"title")
par(usr = op)#############################
points(rnorm(10,-4),rnorm(10,-4))
```

### to put title outside the plot range

```
plot(c(-5,-3),c(-5,-3),type="l")
# title("Title", line = -1)
op<-par("usr","xpd");par(usr=c(0,1,0,1),xpd=TRUE)########
rect(0,1,1,1.1,col="gray80")
text(0.5,1.05,"title")
par(usr=op$usr,xpd=op$xpd)###############################
points(rnorm(10,-4),rnorm(10,-4))
```

### Compare them side by side

```
par(mfrow=c(1,2))

plot(c(-5,-3),c(-5,-3),type="l")
# title("Title", line = -1)
op<-par("usr");par(usr=c(0,1,0,1))########
rect(0,0.9,1,1,col="gray80")
text(0.5,0.95,"title")
par(usr = op)#############################
points(rnorm(10,-4),rnorm(10,-4))

plot(c(-5,-3),c(-5,-3),type="l")
# title("Title", line = -1)
op<-par("usr","xpd");par(usr=c(0,1,0,1),xpd=TRUE)########
rect(0,1,1,1.1,col="gray80")
text(0.5,1.05,"title")
par(usr=op$usr,xpd=op$xpd)###############################
points(rnorm(10,-4),rnorm(10,-4))
```

### Multiple rows and columns

```
dev.size("in")
par(mfrow=c(2,2),
    mar=c(0.5,0.5,2,0.5),
    mgp=c(2,1,0),
    tcl=-0.25)
for(temp in 1:4){
  plot(c(-5,-3),c(-5,-3),type="l")
  op<-par("usr","xpd");par(usr=c(0,1,0,1),xpd=TRUE)########
  rect(0,1,1,1.1,col="gray80")
  text(0.5,1.05,"title")
  par(usr=op$usr,xpd=op$xpd)###############################
  points(rnorm(10,-4),rnorm(10,-4))
}
```

### Use a function to calculate line height

```
plot(c(-5,-3),c(-5,-3),type="l")
# title("Title", line = -1)
op<-par("usr","xpd");par(usr=c(0,1,0,1),xpd=TRUE)########
lineheight<-strheight("title")
rect(0,1,1,1+2*lineheight,col="gray80")
text(0.5,1+lineheight,"title")
par(usr=op$usr,xpd=op$xpd)###############################
points(rnorm(10,-4),rnorm(10,-4))
```

### use functions

```
add_col_title<-function(mytitle){
  op<-par("usr","xpd","xlog","ylog")
  par(usr=c(0,1,0,1),xpd=NA,xlog=FALSE,ylog=FALSE)
  rect(0,1,1,1.1,col="gray90",border="gray")
  text(0.5,1.05,mytitle)
  par(usr=op$usr,xpd=op$xpd,xlog=op$xlog,ylog=op$ylog)
}

add_row_title<-function(mytitle){
  op<-par("usr","xpd","xlog","ylog")
  par(usr=c(0,1,0,1),xpd=NA,xlog=FALSE,ylog=FALSE)
  rect(1,0,1.1,1,col="gray90",border="gray")
  text(1.05,0.5,mytitle,srt=270)
  par(usr=op$usr,xpd=op$xpd,xlog=op$xlog,ylog=op$ylog)
}
```

```
color_levels<-function(x){
  if(is.null(levels(x)))return(NULL)
  x_levels<-levels(x)
  n_levels<-length(x_levels)
  x_hues<-seq(15,375,length=n_levels+1)
  x_colors<-hcl(h=x_hues,l=65,c=100)[1:n_levels]
  names(x_colors)<-x_levels
  x_colors
}

```
