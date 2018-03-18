# Wiskunde_Maze

        private void Solve(int level, int r, int c)
        {
            // vul hier de oplossing in voor het doorlopen van de doolhof
            // ...

            //TODO: zorgen dat de maze niet stopt als je direct naar boven loopt naar de uitgang

            if (!In2DArrayBounds(r, c) && !solutionFound)
            {
                solutionFound = true;
                numberOfSolutionCells++;
                solutionPad[numberOfSolutionCells] = r * cellMatrix.GetLength(1) + c;
                Console.WriteLine("gevonden!!!!!!!!!!!!!!!!!!!!!!!");
                return;
            }

            if (pad[r * squareSizeW + c])
            {
                Console.WriteLine("Al een keer gecheckt");
            }
            else
            {
                //Add path to checked paths
                pad[r * squareSizeW + c] = true;

                if (!((cellMatrix[r, c] & 8) > 0) && !solutionFound)//bottom side open?
                {
                    Console.WriteLine("Move down --> row: {0}, column: {1}", r + 1, c);
                    Solve(level, r + 1, c);

                    //if solution found, add the cell to the solutionPath
                    if (solutionFound)
                    {
                        numberOfSolutionCells++;
                        solutionPad[numberOfSolutionCells] = r * cellMatrix.GetLength(1) + c;
                    }
                }
                if (!((cellMatrix[r, c] & 4) > 0) && !solutionFound)//right side open?
                {
                    Console.WriteLine("Move right --> row: {0}, column: {1}", r, c + 1);
                    Solve(level, r, c + 1);
                    if (solutionFound)
                    {
                        numberOfSolutionCells++;
                        solutionPad[numberOfSolutionCells] = r * cellMatrix.GetLength(1) + c;
                    }
                }
                if (!((cellMatrix[r, c] & 1) > 0) && !solutionFound)//left side open?
                {
                    Console.WriteLine("Move left --> row: {0}, column: {1}", r, c - 1);
                    Solve(level, r, c - 1);
                    if (solutionFound)
                    {
                        numberOfSolutionCells++;
                        solutionPad[numberOfSolutionCells] = r * cellMatrix.GetLength(1) + c;
                    }
                }
                if (!((cellMatrix[r, c] & 2) > 0) && !solutionFound)//top side open?
                {
                    Console.WriteLine("Move up --> row: {0}, column: {1}", r - 1, c);
                    Solve(level, r - 1, c);
                    if (solutionFound)
                    {
                        numberOfSolutionCells++;
                        solutionPad[numberOfSolutionCells] = r * cellMatrix.GetLength(1) + c;
                    }
                }

            }
        }

        private bool In2DArrayBounds(int x, int y)
        {
            if (x < cellMatrix.GetLowerBound(0) ||
                x > cellMatrix.GetUpperBound(0) ||
                y < cellMatrix.GetLowerBound(1) ||
                y > cellMatrix.GetUpperBound(1)) return false;
            return true;
        }
        #endregion

    }
}
