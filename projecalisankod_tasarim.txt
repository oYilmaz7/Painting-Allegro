    #include <stdio.h>
    #include <stdlib.h>
    #include <allegro.h>
/*
    First select a figure. And right click for starting point and left click for end point for make figure.(Square, rect, triangle, line, circle)
    Left click on buckets tick box, makes bucket is active.
    Right click on buckets tick box, makes bucket is passive.




*/





    void init() {
        int depth, res;
        allegro_init();
        depth = desktop_color_depth();
        if (depth == 0) depth = 32;
        set_color_depth(depth);
        res = set_gfx_mode(GFX_AUTODETECT_WINDOWED, 1280, 788, 0, 0);

        // BACKGROUNDS AND ICON IMAGES
        BITMAP * top = load_bitmap("top.bmp", NULL);

        BITMAP * beyaz = load_bitmap("beyaz.bmp", NULL);
        BITMAP * gri = load_bitmap("gri.bmp", NULL);
        BITMAP * kahve = load_bitmap("kahve.bmp", NULL);
        BITMAP * kirmizi = load_bitmap("kirmizi.bmp", NULL);
        BITMAP * mavi = load_bitmap("mavi.bmp", NULL);
        BITMAP * mor = load_bitmap("mor.bmp", NULL);
        BITMAP * sari = load_bitmap("sari.bmp", NULL);
        BITMAP * siyah = load_bitmap("siyah.bmp", NULL);
        BITMAP * turuncu = load_bitmap("turuncu.bmp", NULL);
        BITMAP * yesil = load_bitmap("yesil.bmp", NULL);

        BITMAP * circle = load_bitmap("circle.bmp", NULL);
        BITMAP * eraser = load_bitmap("eraser.bmp", NULL);
        BITMAP * line = load_bitmap("line.bmp", NULL);
        BITMAP * open = load_bitmap("open.bmp", NULL);
        BITMAP * pencil = load_bitmap("pencil.bmp", NULL);
        BITMAP * save = load_bitmap("save.bmp", NULL);
        BITMAP * square = load_bitmap("square.bmp", NULL);
        BITMAP * triangle = load_bitmap("triangle.bmp", NULL);




        //DESIGN
        blit(top, screen, 0, 0, 0, 0, 1280, 68);

        blit(pencil, screen, 0, 0, 10, 0+10, 48, 48);
        blit(line, screen, 0, 0, 48+20, 0+10, 48, 48);
        blit(eraser, screen, 0, 0, 96+30, 0+10, 48, 48);
        blit(triangle, screen, 0, 0, 144+40, 0+10, 48, 48);
        blit(square, screen, 0, 0, 192+50, 0+10, 48, 48);
        blit(circle, screen, 0, 0, 240+60, 0+10, 48, 48);
        blit(open, screen, 0, 0, 288+70, 0+10, 48, 48);
        blit(save, screen, 0, 0, 336+80, 0+10, 48, 48);

        blit(siyah, screen, 0, 0, 500, 10, 24, 24);
        blit(gri, screen, 0, 0, 524, 10, 24, 24);
        blit(kahve, screen, 0, 0, 548, 10, 24, 24);
        blit(kirmizi, screen, 0, 0, 572, 10, 24, 24);
        blit(turuncu, screen, 0, 0, 596, 10, 24, 24);
        blit(beyaz, screen, 0, 0, 500, 34, 24, 24);
        blit(mor, screen, 0, 0, 524, 34, 24, 24);
        blit(sari, screen, 0, 0, 548, 34, 24, 24);
        blit(yesil, screen, 0, 0, 572, 34, 24, 24);
        blit(mavi, screen, 0, 0, 596, 34, 24, 24);


        if (res != 0) {
            allegro_message(allegro_error);
            exit(-1);
        }

        install_timer();
        install_keyboard();
        install_mouse();
        set_window_title("Painting");
        show_mouse(screen);
        show_os_cursor(screen);
    }



    int main()
    {


        init();
        BITMAP * arkaplan = load_bitmap("background.bmp", NULL);

        blit(arkaplan, screen, 0, 0, 0, 68, 1280, 720);

        BITMAP * kaydedilen = load_bitmap("image.bmp", NULL);


        BITMAP *bmp;
        PALETTE pal;
        PALETTE palette;

        int pos_x=0;
        int pos_y=68;
        ;

        BITMAP * bucket_0 = load_bitmap("bucket_0.bmp", NULL);
        BITMAP * bucket_1 = load_bitmap("bucket_1.bmp", NULL);
        blit(bucket_0, screen, 0, 0, 630, 10, 48, 48);


        int araclar[10]= {0,1,2,3,4,5}; //TOOLS
        int arac;
        int sonarac;    //LAST SELECTION
        int sonrenk;    //LAST COLOR
        int secim=0;    //SELECTION


        //COLORS
        int siyah = makecol(0, 0, 0);
        int renk=siyah;     //COLOR=BLACK
        int gri = makecol(140, 140, 140);
        int kahve = makecol(139, 69, 19);
        int kirmizi = makecol(255, 0, 0);
        int turuncu = makecol(255, 192, 0);
        int beyaz = makecol(255, 255, 255);
        int mor = makecol(128, 0, 128);
        int sari = makecol(255, 255, 0);
        int yesil = makecol(0, 255, 0);
        int mavi = makecol(0, 0, 255);


        sonarac=araclar[0];
        sonrenk=renk;


        //IT SAVES LAST SELECTION
    dongu:
        arac=sonarac;
        renk=sonrenk;


        while(!key[KEY_ESC]){


                        if (mouse_b & 2){

                pos_x=mouse_x;
                pos_y=mouse_y;


            }


        //CLICK FOR SELECTION
        if (mouse_x>10 && mouse_x<58 && mouse_y>10 && mouse_y<58 && (mouse_b & 1) ) {
        printf("Kalem");
        arac=araclar[0];

        }

        if (mouse_x>68 && mouse_x<116 && mouse_y>10 && mouse_y<58 && (mouse_b & 1) ) {
        printf("Cizgi");
        arac=araclar[1];
        }


        if (mouse_x>126 && mouse_x<174 && mouse_y>10 && mouse_y<58 && (mouse_b & 1) ) {
        printf("Silgi");
        arac=araclar[2];
        }

        if (mouse_x>184 && mouse_x<232 && mouse_y>10 && mouse_y<58 && (mouse_b & 1) ) {
        printf("Ucgen");
        arac=araclar[3];
        }

        if (mouse_x>242 && mouse_x<290 && mouse_y>10 && mouse_y<58 && (mouse_b & 1) ) {
        printf("Kare");
        arac=araclar[4];
        }

        if (mouse_x>300 && mouse_x<348 && mouse_y>10 && mouse_y<58 && (mouse_b & 1) ) {
        printf("Daire");
        arac=araclar[5];
        }

        if (mouse_x>358 && mouse_x<406 && mouse_y>10 && mouse_y<58 && (mouse_b & 1) ) {
        printf("Ac");



          if (!bmp)


            blit(kaydedilen, screen, 0, 0, 0, 68, 1280, 720);

          destroy_bitmap(bmp);


        }

        if (mouse_x>416 && mouse_x<464 && mouse_y>10 && mouse_y<58 && (mouse_b & 1) ) {
        printf("Kaydet");

        sonrenk=renk;
        sonarac=arac;

         get_palette(pal);
         bmp = create_sub_bitmap(screen, 0, 68, 1280, 788);
         save_bitmap("image.bmp", bmp, NULL);
         destroy_bitmap(bmp);
         printf("Kaydedildi");
         goto dongu;
        }


        //CLICK FOR SELECTION OF COLOR
        if (mouse_x>500 && mouse_x<524 && mouse_y>10 && mouse_y<34 && (mouse_b & 1) ) {
        printf("Siyah");
        renk=siyah;
        }

        if (mouse_x>524 && mouse_x<548 && mouse_y>10 && mouse_y<34 && (mouse_b & 1) ) {
        printf("Gri");
        renk=gri;
        }

        if (mouse_x>548 && mouse_x<572 && mouse_y>10 && mouse_y<34 && (mouse_b & 1) ) {
        printf("Kahverengi");
        renk=kahve;
        }


        if (mouse_x>572 && mouse_x<596 && mouse_y>10 && mouse_y<34 && (mouse_b & 1) ) {
        printf("Kirmizi");
        renk=kirmizi;
        }


        if (mouse_x>596 && mouse_x<620 && mouse_y>10 && mouse_y<34 && (mouse_b & 1) ) {
        printf("Turuncu");
        renk=turuncu;
        }

        if (mouse_x>500 && mouse_x<524 && mouse_y>34 && mouse_y<58 && (mouse_b & 1) ) {
        printf("Beyaz");
        renk=beyaz;
        }

        if (mouse_x>524 && mouse_x<548 && mouse_y>34 && mouse_y<58 && (mouse_b & 1) ) {
        printf("Mor");
        renk=mor;
        }

        if (mouse_x>548 && mouse_x<572 && mouse_y>34 && mouse_y<58 && (mouse_b & 1) ) {
        printf("Sari");
        renk=sari;
        }


        if (mouse_x>572 && mouse_x<596 && mouse_y>34 && mouse_y<58 && (mouse_b & 1) ) {
        printf("Yesil");
        renk=yesil;
        }


        if (mouse_x>596 && mouse_x<620 && mouse_y>34 && mouse_y<58 && (mouse_b & 1) ) {
        printf("Mavi");
        renk=mavi;
        }

        if (mouse_x>630 && mouse_x<678 && mouse_y>10 && mouse_y<58 && (mouse_b & 1) ) {


        if (secim==0) {

            secim=1;
            blit(bucket_1, screen, 0, 0, 630, 10, 48, 48);
            printf("Kutu ekle");
        }

        }


        if (mouse_x>630 && mouse_x<678 && mouse_y>10 && mouse_y<58 && (mouse_b & 2) ) {


        if (secim==1) {

            secim=0;
            blit(bucket_0, screen, 0, 0, 630, 10, 48, 48);
            printf("Kutu kaldir");
        }

        }




        //CLICK FOR PAINTING

        if (mouse_x>0 && mouse_x<1280 && mouse_y>68 && mouse_y<788 && (mouse_b & 1) ) {


        if (arac==araclar[0]) {
         circlefill(screen,mouse_x,mouse_y, 3,renk);
        }

        else if (arac==araclar[1]) {

            if (mouse_b & 1) {
            line(screen, pos_x, pos_y, mouse_x, mouse_y, renk);
            }
        }




        else if (arac==araclar[2]) {
         circlefill(screen,mouse_x,mouse_y, 8,beyaz);
        }



        else if (arac==araclar[3]) {

        if (mouse_b & 1) {

        if (secim==0) {
        line(screen, (mouse_x+pos_x)/2, pos_y,pos_x, mouse_y, renk);
        line(screen, pos_x, mouse_y, mouse_x, mouse_y, renk);
        line(screen, (mouse_x+pos_x)/2, pos_y, mouse_x, mouse_y, renk);
        }
        else if (secim==1) {

            triangle(screen, (mouse_x+pos_x)/2, pos_y, pos_x, mouse_y, mouse_x, mouse_y, renk);
        }

        //



        }
        }

        else if (arac==araclar[4]) {

        if (secim==0) {

            rect(screen,pos_x,pos_y,mouse_x,mouse_y,renk);
        }

        else if (secim==1) {

            rectfill(screen,pos_x,pos_y,mouse_x,mouse_y,renk);

        }


        }

        else if (arac==araclar[5]) {


            if (secim==0) {

                circle(screen, (pos_x+mouse_x)/2, (pos_y+mouse_y)/2, (mouse_y-pos_y)/2, renk);
            }

            else if (secim==1) {

                circlefill(screen, (pos_x+mouse_x)/2, (pos_y+mouse_y)/2, (mouse_y-pos_y)/2, renk);
            }



        }



        rest(1);


        }









        }


        return 0;
    }

    END_OF_MAIN()
