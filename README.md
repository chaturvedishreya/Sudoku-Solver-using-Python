# Sudoku-Solver-using-Python
Grid = [
          ['.', '.', '2', '3'],\n","
          ['.', '.', '.', '.'],\n","
          ['.', '.', '.', '.'],\n","
          ['3', '4', '.', '.']
                                 ]\n","
    "\n",
    "elements = ['1','2','3','4']"


def get_rows(new_Grid):\n",                       // get_rows a function for retrieving the address and value for row elements of the grid.
        rows = []\n",
        for i in range(0,4):\n",
            row = {}\n",
            for y in range(0,4):\n",
                row[(i,y)] = new_Grid[i][y]\n",
            rows.append(row)\n",
        return rows\n",

def get_cols(new_Grid):\n",                       // get_cols a function for retrieving the address and value for column elements of the grid.
        cols = []\n",
        for i in range(0,4):\n",
            col = {}\n",
            for x in range(0,4):\n",
                col[(x,i)] = new_Grid[x][i]\n",
            cols.append(col)\n",
        return cols"

square_indx = [
                 [(0,1),(0,1)],\n","
                 [(0,1),(2,3)],\n","
                 [(2,3),(0,1)],\n","
                 [(2,3),(2,3)] 
                                     ]\n",         // [0,1] for rows range &[0,1] for columns range for 1st inner-square 
                                                   // [0,1]for rows range & [2,3] columns range for 2nd inner square and so on..
                                                      

    

    def get_squares(new_Grid):\n,
     squares = [ ]\n",                        // function get_squares for getting the inner square for a particular address value of the grid.
        for i in range(0,4):\n",
            square = { }\n",
            for x in square_indx[i][0]:\n",
                for y in square_indx[i][1]:\n",
                    square[(x,y)] = new_Grid[x][y]\n",
            squares.append(square)\n",
        return squares"
    
    def get_all_related_cells(new_Grid):\n",
        squares = get_squares(new_Grid)\n",      // get_all_related_cells is a function to retrieve all the related row element, column elements and the                   rows = get_rows(new_Grid)\n",               square elements.
        cols = get_cols(new_Grid)\n",
        all_vec = squares + rows + cols\n",
        return all_vec"

    def get_new_r_c(r, c):\n",
        if c==3:\n",                             // get_new_r_c is a function to jump to the next cell/element after checking and completing the current cell.
            if r==3:\n",
                new_r = r\n",
                new_c = c\n",
            else:\n",
                new_c = 0\n",
                new_r = r+1\n",
        else:\n",
            new_r = r\n",
            new_c = c+1\n",
        return new_r, new_c"
    
    
    def get_legal_for_cell(cell_r, cell_c, new_Grid):\n",         // get_legal_for_cell is a function to get which value can be filled out in a particular cell.
        if new_Grid[cell_r][cell_c]!='.':\n",
            return [None],[None],[None]\n",
    "\n",
        map = { }\n",
        all_vec = get_all_related_cells(new_Grid)\n",
        for a in all_vec:\n",
            if (cell_r, cell_c) in a.keys():\n",
                map.update(a)          # no duplicates\n",
    "\n",
        exist = [ ]\n",
        for m in map:                  # get key from keys\n",
            if not map[m]=='.':\n",
                exist.append(map[m])\n",
    "\n",
        rest = list(set(elements) - set(exist))\n",                  // type cast list into set then subtract and then back to list type
        return rest, exist, map"


   def is_complete(new_Grid):\n",                      // check whether after the changes the sudoku is solved or not
        grid_complete = True\n",
        for r in new_Grid:\n",
            grid_complete = grid_complete and not ('.' in r)\n",
        return grid_complete\n",
    \n",
    def print_grid(new_Grid):\n",
        for item in new_Grid:\n",
            print(item)\n",
        print()"
    
    
    def solve_step_in_sudoko(last_Grid, r, c):\n",
        if is_complete(last_Grid):\n",
            print('Complete:')\n",
            print_grid(last_Grid)\n",
            return 0\n",
        \n",
        legal_for_cell,_ ,_ = get_legal_for_cell(r, c, last_Grid)\n",
    "\n",
        for item in legal_for_cell:\n",
            new_Grid = deepcopy(last_Grid)\n", // so that original remain intact as it is
            if last_Grid[r][c]=='.':\n",
                new_Grid[r][c] = item\n",
            new_r, new_c = get_new_r_c(r, c)\n",
            \n",
            solve_step_in_sudoko(new_Grid, new_r, new_c)\n",
    "\n",
    print('Incomplete:')\n",
    print_grid(Grid)\n",
    solve_step_in_sudoko(Grid, 0, 0)"



     
   


   
   
   








