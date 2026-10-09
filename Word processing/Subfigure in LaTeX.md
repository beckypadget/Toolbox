You need to use the package `subcaption` so that the subfigures work.

```
\usepackage{subcaption}
```

```
\begin{figure}
     \centering
     \begin{subfigure}[b]{0.49\textwidth}
         \centering
         \includegraphics[width=\textwidth]{graph1}
         \caption{ }
         \label{fig:subfig1}
     \end{subfigure}
     \hfill
     \begin{subfigure}[b]{0.49\textwidth}
         \centering
         \includegraphics[width=\textwidth]{graph2}
         \caption{ }
         \label{fig:subfig2}
     \end{subfigure}
	 \caption{Overall caption}
     \label{fig:overall_label}
\end{figure}
```