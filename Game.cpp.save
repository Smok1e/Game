#include <TXLib.h>

//-----------------------------------------------------------------------------

void DrawLevel (HDC Level);

int MoveBall (HDC Level);

void Clear (HDC Level);

bool CheckColor (int x, int y, int r, COLORREF color, HDC level);

int CheckRemote (int *x, int *y, int dt, bool *Collision);

//-----------------------------------------------------------------------------

int main ()

{

    txCreateWindow (500, 500);
    txDisableAutoPause ();

    HDC Level = txLoadImage ("Level.bmp");

    Clear (Level);

    bool close = false;

    while (!close)

    {

        int result = MoveBall (Level);

        if (result == 1)

        {

            txPlaySound ("loh.wav");

        }

        if (result == 2)

        {

            txPlaySound ("win.wav");
            txSleep (500);

        }

        if (result == 0)

        {

            close = true;

        }

    }

    txDeleteDC (Level);

    return 0;

}

void DrawLevel (HDC Level)

{

    txBitBlt (txDC(), 0, 0, 500, 500, Level, 0, 0);

}

int MoveBall (HDC Level)

{

    int x = 10;
    int y = 10;

    double vx = 0;
    double vy = 0;

    int r = 5;

    int dt = 1;

    bool Collision = true;

    while (true)

    {

        Clear (Level);

        txSetColor (TX_LIGHTRED);
        txSetFillColor (TX_LIGHTRED);

        txCircle (x, y, r);

        if (CheckRemote (&x, &y, dt, &Collision) == 0)

        {

            return 0;

        }


        if (CheckColor (x, y, r, TX_WHITE, Level) && Collision)

        {

            return 1;

        }

        if (CheckColor (x, y, r, RGB (0, 0, 255), Level))

        {

            return 2;

        }

        txSleep (1);

    }

}

void Clear (HDC Level)

{

    txSetColor (TX_BLACK);
    txSetFillColor (TX_BLACK);

    txRectangle (0, 0, 500, 500);

    DrawLevel (Level);

}

bool CheckColor2 (int x, int y, int r, COLORREF color, HDC level)
{
    for (double angle = 0; angle < 2 * M_PI; angle+= M_PI / 4)
    {
        int circularX = x + (r) * cos (angle);
        int circularY = y + (r) * sin (angle);

        if (txGetPixel (circularX, circularY) == color)
        {

            return true;

        }

    }

    return false;
}

bool CheckColor (int x, int y, int r, COLORREF color, HDC level)

{

    if (txGetPixel (x + r,        y           ) == color) return true;
    if (txGetPixel (x + r * 0.71, y - r * 0.71) == color) return true;
    if (txGetPixel (x,            y + r       ) == color) return true;
    if (txGetPixel (x - r * 0.71, y - r * 0.71) == color) return true;
    if (txGetPixel (x - r,        y           ) == color) return true;
    if (txGetPixel (x - r * 0.71, y + r * 0.71) == color) return true;
    if (txGetPixel (x,            y + r       ) == color) return true;
    if (txGetPixel (x + r * 0.71, y + r * 0.71) == color) return true;

    return false;

}

int CheckRemote (int* x, int* y, int dt, bool* Collision)

{

    if (GetAsyncKeyState (VK_RIGHT))

    {

        *x = *x + dt;

    }

    if (GetAsyncKeyState (VK_LEFT))

    {

        *x = *x - dt;

    }

    if (GetAsyncKeyState (VK_UP))

    {

        *y = *y - dt;

    }

    if (GetAsyncKeyState (VK_DOWN))

    {

        *y = *y + dt;

    }

    if (GetAsyncKeyState (VK_ESCAPE))

    {

        return 0;

    }

    if (GetAsyncKeyState (VK_TAB))

    {

        if (Collision)

        {

            *Collision = false;

        }

        else

        {

            *Collision = true;

        }

        txSleep(500);

    }

    return 1;

}

