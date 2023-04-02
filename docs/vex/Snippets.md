!!! note
    Point Wrangle
    Bisects a vector fixing the first and last points
```c
// Get the next points N
vector prevPointP = point(0, 'P', @ptnum + 1);
vector nextPointP = point(0, 'P', @ptnum - 1);

// Create the bisected vector
v@N = cross(normalize(nextPointP - prevPointP), v@up);

// Check if it's the fist point
if (@ptnum == 0){
    // Create the bisected vector
    v@N = -cross(normalize(prevPointP - @P), v@up);
}

// Check if it's the last point
if (@ptnum == @numpt - 1){
    vector vec = normalize(-cross(@P - point(0, 'P', @ptnum - 1), {0, 1, 0}));
    @N = vec;
}
``` 
!!! note
    Prim Wrangle
    Makes a primitive polywire sag good idea to resample it first

```c
int    Count, Pt_List[];
float  Fitted_Pt_Num, Ramped_Pt_Num;
vector Modifier;

Pt_List =  primpoints(geoself(), 0);    

for(Count = 0; Count < len(Pt_List); Count++){
    Modifier      = set(0,0,0);
    Fitted_Pt_Num = efit(Count, 0, (len(Pt_List) - 1), 0, 1);
    Ramped_Pt_Num = chramp("sag_control", Fitted_Pt_Num);
    Modifier.y    = -(Ramped_Pt_Num * chf("sag_multiplier"));
    //Modifier      = set(1,Ramped_Pt_Num,1);
    setpointattrib(geoself(), "P", Pt_List[Count], Modifier, "add");
}
```

!!! note
    Prim wrangle (Points Line N at next point)
    Get Point Numbers (Should only ever be 2)
```c
int points[] = primpoints(0, @primnum);
// resize(points, 2);

// Get P of each point
vector points_P[];
foreach (int point; points) {
    vector P = point(0, 'P', point);
    push(points_P, P);
}

setpointattrib(0, 'N', points[0], (points_P[1] - points_P[0]));
setpointattrib(0, 'N', points[1], (points_P[0] - points_P[1]));
```

!!!note

    Look for a value in an array
    You should use find() instead
```c
int contains(int array[]; int value){
    foreach (int check_val; array){
        if (check_val == value){
            return 1;
        }
    }
    return 0;
}
```

!!! note
    Prim Wrangle
    This vex wrangle will find all the connected prim neighbors of an object
```c
int     prim_edge, edge, prim, i, n, num;
string  neighbours = "";

i = 0;
prim_edge = primhedge(@OpInput1, @primnum);
while(i < primvertexcount(@OpInput1, @primnum))
{
    num = hedge_equivcount(@OpInput1, prim_edge);
    n = 0;
    while(n < num)
    {
        edge = hedge_nextequiv(@OpInput1, prim_edge);
        prim = hedge_prim(@OpInput1, edge);
        if(prim != @primnum)
            neighbours += sprintf("%g ", prim);

        prim_edge = edge;
        n++;
    }

    prim_edge = hedge_next(@OpInput1, prim_edge);
    i++;      
}

s@neighbours = neighbours;
```

!!! note
    If a prim @Cd is red return its primnum
```c

int has_red_neighbor(string primnums) {
  foreach(string s_primnum; split(primnums)) {
    int primnum = atoi(s_primnum);
    if (prim(0, 'Cd', primnum) == set(1, 0, 0))
      return primnum;
  }
  return -1;
}
```
```c
int find_non_outerwall_neighbor(string primnums) {
  foreach(string s_primnum; split(primnums)) {
    int primnum = atoi(s_primnum);
    if (prim(0, 'group_outer_walls', primnum) == 0)
      return primnum;
  }
  return -1;
}
```
!!! note
    Get an interger list of the primitive attribute neighbors
```c

int[] get_neighbors_from_primnum(int primnum) {
  int int_neighbors[] = array();
  string neighbors[] = split(prim(0, 'neighbors', primnum));
  foreach(string n_primnum; neighbors) {
    push(int_neighbors, atoi(n_primnum));
  }
  return int_neighbors;
}
```
!!! note
    If a primitive has any neighbor primitive points that share a point with any other neighbor
    that piece is an elbow piece
```c
int is_elbow(int primnum) {
  int seen_points[] = array();
  // Get the neighbors
  int neighbors[] = get_neighbors_from_primnum(primnum);
  foreach(int n_primnum; neighbors) {
    // get the neigbor points
    int neighbor_points[] = primpoints(0, n_primnum);
    foreach(int pointnum; neighbor_points) {
      // If we've seen the point return immediatly
      if (find(seen_points, pointnum) >= 0) {
        return 1;
      }
      // add the seen points to the arry
      push(seen_points, pointnum);
    }
  }
  return 0;
}
```

```c

int[] split_neighbors_to_int_array(string neighbors) {
  int ret_arr[] = array();
  foreach(string primnum; split(neighbors)) {
    push(ret_arr, atoi(primnum));
  }
  return ret_arr;
}
```

```c

int[] get_blue_neighbors(string str_neighbors) {
  int blue_neighbors[] = array();
  int neighbors[] = split_neighbors_to_int_array(str_neighbors);
  foreach(int primnum; neighbors) {
    if (prim(0, 'Cd', primnum) == set(0, 0, 1)) {
      push(blue_neighbors, primnum);
    }
  }
  return blue_neighbors;
}
```

```c
vector get_first_blue_neighbors_vector(int blue_neighbors[]) {
  vector facing_arr[] = array();
  foreach(int primnum; blue_neighbors) {
    vector facing = prim(0, 'facing', primnum);
    push(facing_arr, facing);
  }
  return facing_arr[1];
}
```

```c
int find_first_unseen(int seen_prims[]; int neighbors[]) {
  foreach(int neighbor; neighbors) {
    if (find(seen_prims, neighbor) >= 0) {} else {
      return neighbor;
    }
  }
}
```

!!! note
    OpInput1: is usually just @OpInput1 and primnum is @primnum
```c

string neighbor_prims(string OpInput1; int primnum) {
  int prim_edge, edge, prim, i, n, num;
  int neighbours_arr[] = array();
  string neighbors = "";

  i = 0;
  prim_edge = primhedge(OpInput1, primnum);
  while (i < primvertexcount(OpInput1, primnum)) {
    num = hedge_equivcount(OpInput1, prim_edge);
    n = 0;
    while (n < num) {
      edge = hedge_nextequiv(OpInput1, prim_edge);
      prim = hedge_prim(OpInput1, edge);
      if (prim != primnum) {
        neighbors += sprintf("%s ", prim);
        push(neighbours_arr, prim);;
      }
      prim_edge = edge;
      n++;
    }
    prim_edge = hedge_next(OpInput1, prim_edge);
    i++;
  }
  return neighbors;
}
```

!!! note
    OpInput1: is usually just @OpInput1 and primnum is @primnum

```c
int[] neighbor_prims_i(string OpInput1; int primnum) {
  int prim_edge, edge, prim, i, n, num;
  int neighbours_arr[] = array();
  i = 0;
  prim_edge = primhedge(OpInput1, primnum);
  while (i < primvertexcount(OpInput1, primnum)) {
    num = hedge_equivcount(OpInput1, prim_edge);
    n = 0;
    while (n < num) {
      edge = hedge_nextequiv(OpInput1, prim_edge);
      prim = hedge_prim(OpInput1, edge);
      if (prim != primnum) {
        push(neighbours_arr, prim);;
      }
      prim_edge = edge;
      n++;
    }
    prim_edge = hedge_next(OpInput1, prim_edge);
    i++;
  }
  return neighbours_arr;
}
```


```c
vector get_direction_from(int primnum1; int primnum2){
  vector direction =  prim(0,'P', primnum2) - prim(0, 'P', primnum1);
  return normalize(set(direction.x, direction.y, direction.z));
}
```

```c

int is_left(int primnum; int neighbor_primnum){
  if (get_direction_from(primnum, neighbor_primnum) == set(1, 0, 0) ){
    return 1;
  }
  return 0;
}
```

```c

int is_right(int primnum; int neighbor_primnum){
  if (get_direction_from(primnum, neighbor_primnum) == set(-1, 0, 0) ){
    return 1;
  }
  return 0;
}```

```c

int is_above(int primnum; int neighbor_primnum){
  if (get_direction_from(primnum, neighbor_primnum) == set(0, 0, 1) ){
    return 1;
  }
  return 0;
}
```

```c
int is_below(int primnum; int neighbor_primnum){
  vector dir = get_direction_from(primnum, neighbor_primnum);
  if (dir == set(0, 0, -1)){
    return 1;
  }
  return 0;
}
```

```c
int has_neighbors_above(int primnum){
  int neighbors[] = get_neighbors_from_primnum(primnum);
  foreach (int neighbor_prim; neighbors){
      if (is_above(primnum, neighbor_prim)){
        return 1;
      }
  }
  return 0;
}
```

```c
int has_neighbors_left(int primnum){
  int neighbors[] = get_neighbors_from_primnum(primnum);
  foreach (int neighbor_prim; neighbors){
      if (is_left(primnum, neighbor_prim)){
        return 1;
      }
  }
  return 0;
}
```

```c
int has_neighbors_right(int primnum){
  int neighbors[] = get_neighbors_from_primnum(primnum);
  foreach (int neighbor_prim; neighbors){
      if (is_right(primnum, neighbor_prim)){
        return 1;
      }
  }
  return 0;
}
```

```c
int has_neighbors_below(int primnum){
  int neighbors[] = get_neighbors_from_primnum(primnum);
  foreach (int neighbor_prim; neighbors){
      if (is_below(primnum, neighbor_prim)){
        return 1;
      }
  }
  return 0;
}
```

```c
int[] get_shape_array(int primnum){
  int shape_array[] = array();
  push(shape_array, has_neighbors_left(primnum));
  push(shape_array, has_neighbors_right(primnum));
  push(shape_array, has_neighbors_above(primnum));
  push(shape_array, has_neighbors_below(primnum));
  return shape_array;
}
```

```c
int array_equivelant(int arr1[]; int arr2[]){
  int i = 0;
  foreach(int val; arr2) {
    // If a value doesn't match return back false
    if (val != arr1[i]){
      return 0;
    }
    i += 1;
  }
  // All the values match return true
  return 1;
}
```