---
layout: post
tag: 
  - Tikz
  - latex
comments: true
date: 2018-04-28
title: A Tutorial for of Tikz 
---

``` latex
\documentclass[11pt]{article}

\usepackage{tikz}
\usetikzlibrary{arrows}

\begin{document}

% simple straight lines, scales
\begin{tikzpicture}%[xscale=1,yscale=2]
	\draw (0,0) -- (1,2) -- (-1,3) -- (-2,1) -- (0,0);
	\draw [help lines] (-2,0) grid (1,3);
\end{tikzpicture}

% arrows and the like
\begin{tikzpicture}
	\draw [|->] (0,0) -- (2,0);
	\draw [->] (0,1) -- (2,1);
	\draw [<->] (0,2) -- (2,2);
    \draw [<->] (-1,3) -- (-1,-1) -- (3,-1);
\end{tikzpicture}

% linewidth, colors, dashes and dots
\begin{tikzpicture}
	\draw [red, <->] (0,2) -- (0,0) -- (4,0); 
	\draw [yellow, help lines] (0,1.5) -- (3,0); 
	\draw [dashed, ultra thick] (0,0) -- (2,2); 
	\draw [dotted, rounded corners, thick] (1,0) -- (1,1) -- (0,1); 
\end{tikzpicture}

% inline pictures
I want to create a yellow block here \begin{tikzpicture} \draw [yellow, line width = 0.5cm] (0,0)--(.5,0); \end{tikzpicture}.

% curves and shapes
\begin{tikzpicture}
  \draw [blue, thick] (0,0) rectangle (3,4);
  \draw [red, thick] (3,2) circle [radius=2];
  \draw [gray, thick] (0,0) arc [radius=3, start angle=180, end angle=90];
\end{tikzpicture}

% smooth
\begin{tikzpicture}
\draw [<->,thick, cyan] (0,0) to [out=90,in=180] (1,1) to [out=0,in=180] (2.5,0) to [out=0,in=-135] (4,1) ;
\draw [help lines] (0,0) grid (4,1);
\end{tikzpicture}

% plotting function
\begin{tikzpicture}
	\draw [<->] (0,5) -- (0,0) -- (3,0);
	\draw [green, ultra thick, domain=0:2] plot (\x, {0.5+\x^2});
\end{tikzpicture}
\begin{tikzpicture}[yscale=1.5] 
\draw [help lines, <->] (0,0) -- (6.5,0); 
\draw [help lines, ->] (0,-1.1) -- (0,1.1); 
\draw [green,domain=0:2*pi] plot (\x, {(sin(\x r)* ln(\x+1))/2}); 
\draw [red,domain=0:pi] plot (\x, {sin(\x r)}); 
\draw [blue, domain=pi:2*pi] plot (\x, {cos(\x r)*exp(\x/exp(2*pi))}); 
\end{tikzpicture}


% \begin{tikzpicture}[x={(0.866cm,-0.5cm)}, y={(0.866cm,0.5cm)}, z={(0cm,1cm)}, scale=1.0,
%     %Option for nice arrows
%     >=stealth, %
%     inner sep=0pt, outer sep=2pt,%
%     axis/.style={thick,->},
%     wave/.style={thick,color=#1,smooth},
%     polaroid/.style={fill=black!60!white, opacity=0.3},
% ]
%     % Colors
%     \colorlet{darkgreen}{green!50!black}
%     \colorlet{lightgreen}{green!80!black}
%     \colorlet{darkred}{red!50!black}
%     \colorlet{lightred}{red!80!black}

%     % Frame
%     \coordinate (O) at (0, 0, 0);
%     \draw[axis] (O) -- +(14, 0,   0) node [right] {x};
%     \draw[axis] (O) -- +(0,  2.5, 0) node [right] {y};
%     \draw[axis] (O) -- +(0,  0,   2) node [above] {z};

%     \draw[thick,dashed] (-2,0,0) -- (O);

%     % monochromatic incident light with electric field
%     \draw[wave=blue, opacity=0.7, variable=\x, samples at={-3,-2.75,...,0}]
%         plot (\x, { cos(1.0*\x r)*sin(2.0*\x r)}, { sin(1.0*\x r)*sin(2.0*\x r)})
%         plot (\x, {-cos(1.0*\x r)*sin(2.0*\x r)}, {-sin(1.0*\x r)*sin(2.0*\x r)});

%     \foreach \x in{-2,-1.75,...,0}{
%         \draw[color=blue, opacity=0.7,->]
%             (\x,0,0) -- (\x, { cos(1.0*\x r)*sin(2.0*\x r)}, { sin(1.0*\x r)*sin(2.0*\x r)})
%             (\x,0,0) -- (\x, {-cos(1.0*\x r)*sin(2.0*\x r)}, {-sin(1.0*\x r)*sin(2.0*\x r)});
%     }

%     \filldraw[polaroid] (0,-2,-1.5) -- (0,-2,1.5) -- (0,2,1.5) -- (0,2,-1.5) -- (0,-2,-1.5)
%         node[below, sloped, near end]{Polaroid};%

%     %Direction of polarization
%     \draw[thick,<->] (0,-1.75,-1) -- (0,-0.75,-1);

%     % Electric field vectors
%     \draw[wave=blue, variable=\x,samples at={0,0.25,...,6}]
%         plot (\x,{sin(2*\x r)},0)node[anchor=north]{$\vec{E}$};

%     %Polarized light between polaroid and thin section
%     \foreach \x in{0, 0.25,...,6}
%         \draw[color=blue,->] (\x,0,0) -- (\x,{sin(2*\x r)},0);

%     \draw (3,1,1) node [text width=2.5cm, text centered]{Polarized light};

%     %Crystal thin section
%     \begin{scope}[thick]
%         \draw (6,-2,-1.5) -- (6,-2,1.5) node [above, sloped, midway]{Crystal section}
%                 -- (6, 2, 1.5) -- (6, 2, -1.5) -- cycle % First face
%             (6,  -2, -1.5) -- (6.2, -2,-1.5)
%             (6,   2, -1.5) -- (6.2,  2,-1.5)
%             (6,  -2,  1.5) -- (6.2, -2, 1.5)
%             (6,   2,  1.5) -- (6.2,  2, 1.5)
%             (6.2,-2, -1.5) -- (6.2, -2, 1.5) -- (6.2, 2, 1.5) 
%                 -- (6.2, 2, -1.5) -- cycle; % Second face

%         %Optical indices
%         \draw[darkred, ->]       (6.1, 0, 0) -- (6.1, 0.26,  0.966) node [right] {$n_{g}'$}; % index 1
%         \draw[darkred, dashed]   (6.1, 0, 0) -- (6.1,-0.26, -0.966); % index 1
%         \draw[darkgreen, ->]     (6.1, 0, 0) -- (6.1, 0.644,-0.173) node [right] {$n_{p}'$}; % index 2
%         \draw[darkgreen, dashed] (6.1, 0, 0) -- (6.1,-0.644, 0.173); % index 2
%     \end{scope}

%     %Rays leaving thin section
%     \draw[wave=darkred,   variable=\x, samples at={6.2,6.45,...,12}] 
%         plot (\x, {0.26*0.26*sin(2*(\x-0.5) r)},  {0.966*0.26*sin(2*(\x-0.5) r)});  %n'g-oriented ray
%     \draw[wave=darkgreen, variable=\x, samples at={6.2,6.45,...,12}]
%         plot (\x, {0.966*0.966*sin(2*(\x-0.1) r)},{-0.26*0.966*sin(2*(\x-0.1) r)}); %n'p-oriented ray
%     \draw (10,1,1) node [text width=2.5cm, text centered] {Polarized and dephased light};

%     \foreach \x in{6.2,6.45,...,12} {
%         \draw[color=darkgreen, ->] (\x, 0, 0) --
%             (\x, {0.966*0.966*sin(2*(\x-0.1) r)}, {-0.26*0.966*sin(2*(\x-0.1) r)});
%         \draw[color=darkred,   ->] (\x, 0, 0) --
%             (\x, {0.26*0.26*sin(2*(\x-0.5) r)}, {0.966*0.26*sin(2*(\x-0.5) r)});
%     }

%     %Second polarization
%     \draw[polaroid]   (12, -2,  -1.5) -- (12, -2,   1.5)  %Polarizing filter
%         node [above, sloped,midway] {Polaroid} -- (12, 2, 1.5) -- (12, 2, -1.5) -- cycle;
%     \draw[thick, <->] (12, -1.5,-0.5) -- (12, -1.5, 0.5); %Polarization direction

%     %Light leaving the second polaroid
%     \draw[wave=lightgreen,variable=\x, samples at={12, 12.25,..., 14}]
%         plot (\x,{0}, {0.966*0.966*0.26*sin(2*(\x-0.5) r)}); %n'g polarized ray
%     \draw[wave=lightred,  variable=\x, samples at={12, 12.25,..., 14}]
%         plot (\x,{0}, {-0.26*0.966*sin(2*(\x-0.1) r)});      %n'p polarized ray

%     \node[align=justify, text width=14cm, anchor=north west, yshift=-2mm] at (current bounding box.south west)
%         {Light behavior in a petrographic microscope with light polarizing
%         device. Only one incident wavelength is shown (monochromatic light).
%         The magnetic field, perpendicular to the electric one, is not drawn.};
% \end{tikzpicture}
\end{document}
``` 